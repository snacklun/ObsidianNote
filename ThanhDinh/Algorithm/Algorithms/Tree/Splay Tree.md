## 📝 Algorithm Explanation Note Template: Splay Tree

|**Field**|**Detail / Placeholder**|
|---|---|
|**Algorithm Name**|Splay Tree|
|**Category**|Searching, Self-Adjusting Binary Search Tree|
|**Author/Observer**|Gemini AI|
|**Date of Observation**|December 2025|
|**Source/Reference**|Amortized Analysis and Data Structures|

---

## I. Overview and Purpose

### 1. Goal

Describe the primary objective. _What problem does this algorithm solves?_

> **Goal:** To optimize performance based on the **frequency of access**. It is a self-adjusting BST that moves the most recently accessed item to the root, making subsequent accesses to that item very fast.

### 2. Constraints / Prerequisites

What conditions must the input data meet for the algorithm to work?

> **Constraints:** Requires data to be searchable. The primary measure of performance is **amortized time** (average time over a sequence of operations), rather than worst-case time for a single operation.

---

## II. Core Logic and Mechanics

### 3. Key Data Structures

Identify the essential structures used.

> **Key Structures:** A standard Binary Search Tree structure. It requires **no extra metadata** (like color or height) in the nodes.

### 4. Step-by-Step Procedure

1. **Access:** Whenever a node ($x$) is searched for, inserted, or deleted, it must first be brought to the **root** of the tree.
    
2. **Splaying:** The process of moving node $x$ to the root is called **splaying**. It is done using a series of specialized double rotations (Zig-Zig, Zig-Zag) or single rotations (Zig) based on the current position of $x$ and its parent/grandparent.
    
3. **Insertion/Deletion:** After the relevant key is splayed to the root, insertion is trivial (create a new root) and deletion is simple (delete the root, then combine the two subtrees using a final splay operation).
    

### 5. Illustration with detail steps/Example with explain/Code details in C# with comment

> **Illustration Focus:** Show the two key splaying operations: **Zig-Zig** (when $x$, parent, and grandparent are in a line) and **Zig-Zag** (when they form a bend). These are done to ensure good amortized performance.

---

## III. Performance Analysis

### 6. Time Complexity

|**Metric**|**Complexity**|**Rationale**|
|---|---|---|
|**Single Operation (Worst Case)**|$O(N)$|If the accessed node is very deep in a highly skewed tree, a single splay operation can take linear time.|
|**Amortized (Average over sequence)**|$O(\log N)$|Over a long sequence of operations, the cost of the expensive $O(N)$ splay is balanced out by the many fast $O(1)$ accesses to frequently splayed (root) nodes.|
|**Space Complexity**|$O(N)$|Requires only space for the $N$ nodes.|

### 7. Efficiency Notes

Explain why the chosen complexity is achieved (e.g., how the Priority Queue improves performance).

> **Efficiency Notes:** Splay trees are faster than RBTs or AVL trees when the access pattern is **skewed** (some items are accessed much more often than others). The **splaying** operation serves two purposes: it brings the accessed node up (fast future access) and simultaneously reduces the height of the access path for all subsequent nodes (balancing the tree implicitly).