## 📝 Algorithm Explanation Note Template: B-Tree

|**Field**|**Detail / Placeholder**|
|---|---|
|**Algorithm Name**|B-Tree|
|**Category**|Searching, Balanced Tree, External Memory (Disk Storage)|
|**Author/Observer**|Gemini AI|
|**Date of Observation**|December 2025|
|**Source/Reference**|Database Systems / Data Structures Textbooks|

---

## I. Overview and Purpose

### 1. Goal

Describe the primary objective. _What problem does this algorithm solve?_

> **Goal:** To manage sorted data efficiently on **disk storage** (external memory). It minimizes the number of disk accesses (Input/Output operations) required to find, insert, or delete a record, which is the main bottleneck for large datasets.

### 2. Constraints / Prerequisites

What conditions must the input data meet for the algorithm to work?

> **Constraints:** Requires data to be searchable (i.e., keys must be comparable). The tree's order ($M$) must be carefully chosen so that one node's size exactly matches the size of one disk block.

---

## II. Core Logic and Mechanics

### 3. Key Data Structures

Identify the essential structures used.

> **Key Structures:** The tree is composed of nodes, where each node stores a variable number of keys and pointers (references) to child nodes.

### 4. Step-by-Step Procedure

1. **Initialization:** The tree starts with a single root node.
    
2. **Search:** Start at the root. Within the node, use binary search to find the key or determine the pointer to the next child node to follow. Repeat until the leaf node is reached.
    
3. **Insertion:** Insert the new key into the appropriate leaf node.
    
4. **Balancing (Node Splitting):** If the insertion causes a node to exceed the maximum number of allowed keys ($M-1$), the node **splits**. The median key is promoted to the parent node, and the two halves become children of the promoted key.
    
5. **Deletion (Node Merging):** If a deletion causes a node to fall below the minimum number of keys, the node either borrows a key from a sibling or merges with a sibling, pulling a key down from the parent.
    

### 5. Illustration with detail steps/Example with explain/Code details in C# with comment

> **Illustration Focus:** The key operation is **Node Splitting** during insertion, which is what keeps the tree shallow. Since the height of the B-Tree is $O(\log_M N)$, the complexity is dominated by the base $M$, reflecting minimal disk accesses.

![[Pasted image 20251213215830.png]]

## **Step-by-Step B-Tree Operations (Order M)**

Let's assume a **B-Tree of Order 4** ($M=4$).

- **Max Keys per node:** $M-1 = 3$
    
- **Max Children per node:** $M = 4$
    
- **Min Keys per node (non-root):** $\lceil M/2 \rceil - 1 = 1$
    
- **Min Children (non-root):** $\lceil M/2 \rceil = 2$
    

---

### **1. Insertion (Step-by-Step)**

**Goal:** Insert key **`k`**. Always add to a **Leaf Node**.

**Scenario:** We insert keys `10, 20, 5, 6, 12, 30, 7` into an empty tree.

1. **Insert 10, 20:**
    
    - Root is empty. Add `10`. Root: `[10]`.
        
    - Add `20`. Sort it. Root: `[10, 20]`.
        
    - _Status:_ Root has space (Max 3 keys). No split needed.
        
2. **Insert 5:**
    
    - Add `5`. Sort. Root: `[5, 10, 20]`.
        
    - _Status:_ Root is now **FULL** (3 keys).
        
3. **Insert 6 (Split Root):**
    
    - Target node (Root) is full `[5, 10, 20]`. We must split _before_ or _during_ adding `6`.
        
    - **Action:** Split `[5, 10, 20]` at median `10`.
        
        - **Promote Median:** `10` becomes the new Root.
            
        - **Split:** Left child gets `[5]`, Right child gets `[20]`.
            
    - **Insert 6:** `10` > `6` > `5`. Go to Left Child `[5]`. Insert `6`.
        
    - _Result:_
        
        - Root: `[10]`
            
        - Children: `[5, 6]` and `[20]`
            
4. **Insert 12:**
    
    - Compare with Root `10`: `12 > 10`. Go to Right Child `[20]`.
        
    - Insert `12`. Sort. Right Child becomes `[12, 20]`.
        
5. **Insert 30:**
    
    - Compare with Root `10`: `30 > 10`. Go to Right Child `[12, 20]`.
        
    - Insert `30`. Right Child becomes `[12, 20, 30]`.
        
    - _Status:_ Right Child is **FULL**.
        
6. **Insert 7 (Split Child):**
    
    - Compare with Root `10`: `7 < 10`. Go to Left Child `[5, 6]`.
        
    - Insert `7`. Left Child becomes `[5, 6, 7]`.
        
    - _Status:_ Left Child is **FULL**.
        
7. **Insert 15 (Split Internal/Leaf):**
    
    - Compare with Root `10`. Go Right.
        
    - Right Child `[12, 20, 30]` is full. **Split it!**
        
        - Median `20` goes UP to Root.
            
        - Root becomes `[10, 20]`.
            
        - Right Child splits into `[12]` and `[30]`.
            
    - Now Insert `15`:
        
        - Compare with Root `[10, 20]`. `10 < 15 < 20`. Go to Middle Child `[12]`.
            
        - Add `15`. Node becomes `[12, 15]`.
            

---

### **2. Deletion (Step-by-Step)**

**Goal:** Remove key **`k`**. Ensure nodes don't get too empty (underflow).

**Scenario:** Delete from the tree created above.

- Root: `[10, 20]`
    
- Children: `[5, 6, 7]`, `[12, 15]`, `[30]`
    

1. **Simple Deletion (Leaf has extras):** **Delete 6**
    
    - Locate `6` in the first child `[5, 6, 7]`.
        
    - Node has 3 keys (Min is 1). Safe to delete.
        
    - Remove `6`. Node becomes `[5, 7]`.
        
2. **Delete Internal Node (Predecessor/Successor Swap):** **Delete 20**
    
    - `20` is in the Root. We can't delete directly from internal nodes.
        
    - **Swap:** Find immediate successor (smallest value in right subtree) or predecessor. Let's use **Successor**.
        
        - Go to right child of `20` -> `[30]`. Successor is `30`.
            
    - **Replace:** Replace `20` with `30` in Root. Root is `[10, 30]`.
        
    - **Delete Successor:** Now delete `30` from the leaf `[30]`.
        
    - **Underflow!** Leaf `[30]` becomes empty `[]`. (Min keys = 1).
        
    - **Fix Underflow (Borrow):**
        
        - Sibling (middle child) is `[12, 15]`. It has extras!
            
        - **Rotate:** Move `15` up to Root. Move `30` (old root key) down to empty node.
            
        - Wait, the old root key was `30`. Let's re-trace.
            
        - Root `[10, 30]`. Child `[30]` became empty. Sibling `[12, 15]`.
            
        - **Borrow from Left Sibling:**
            
            - Take largest key `15` from sibling.
                
            - Move parent key (`30` at index 1) down to the empty node.
                
            - Move sibling key `15` up to parent.
                
            - New Root: `[10, 15]`.
                
            - Middle Child: `[12]`.
                
            - Right Child: `[30]`.
                
3. **Delete causing Merge (Height reduction):** **Delete 30**
    
    - Locate `30` in Right Child. Remove it. Node becomes empty `[]`.
        
    - **Underflow:**
        
        - Left Sibling `[12]` has only 1 key. Cannot borrow.
            
        - **Action: Merge.**
            
        - Combine: Left Sibling `[12]` + Separator Key from Parent (`15`) + Empty Node.
            
        - New Merged Node: `[12, 15]`.
            
        - Remove `15` from Parent.
            
    - **Check Parent (Root):**
        
        - Parent `[10, 15]` lost `15`. Parent becomes `[10]`.
            
        - Is Parent underflowed? No, Root can have 1 key.
            
    - _Result:_
        
        - Root: `[10]`
            
        - Children: `[5, 7]` and `[12, 15]`
            
4. **Delete 10 (Root collapse):**
    
    - `10` is in Root. Swap with successor `12` (from `[12, 15]`).
        
    - Root becomes `[12]`.
        
    - Delete `12` from leaf `[12, 15]`. Leaf becomes `[15]`.
        
    - All valid.

---

## III. Performance Analysis

### 6. Time Complexity

|**Metric**|**Complexity**|**Rationale**|
|---|---|---|
|**Search/Insert/Delete**|$O(t \cdot \log_M N)$|$N$: total keys. $M$: max children. $t$: time to search within a node. The height is $\log_M N$. $t$ is small but necessary for in-memory work. The complexity highlights the small height, $\log_M N$.|
|**Space Complexity**|$O(N)$|Linear space is required to store all $N$ keys.|

### 7. Efficiency Notes

Explain why the chosen complexity is achieved (e.g., how the Priority Queue improves performance).

> **Efficiency Notes:** B-Trees are shallow and bushy. The large branching factor ($M$) ensures the tree height is extremely small. The primary time cost in a B-Tree is not the CPU time, but the **slow disk access time**. By organizing the node size to exactly match the disk block size, every $\log_M N$ step in the search only requires **one** physical disk read, making it ideal for systems that deal with terabytes of data.

---

## IV. Applications and Review

### 8. Use Cases

Where is this algorithm commonly applied in real-world systems?

> **Use Cases:** Core index structure for **Relational Databases** (e.g., PostgreSQL, Oracle), and large **File Systems** (e.g., NTFS, ext4, XFS).

### 9. Observer Notes / Review Points

Add any specific observations, potential pitfalls, or necessary optimizations for implementation.

> **Observer Notes:** B-Trees are complex to implement correctly due to the splitting and merging logic required to maintain strict balance properties (minimum fill factor). The goal is always to maximize $M$ based on hardware characteristics.