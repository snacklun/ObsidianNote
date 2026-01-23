
### Algorithms Grouped by Type

### 1. **Sorting Algorithms**

Algorithms that arrange elements in a specific order (e.g., ascending or descending).

- **Comparison-Based Sorting**:
    - Bubble Sort: Repeatedly swaps adjacent elements if out of order (O(n²)).
    - Selection Sort: Repeatedly selects the minimum element and places it at the beginning (O(n²)).
    - Insertion Sort: Builds the sorted array one element at a time (O(n²)).
    - Merge Sort: Divides the array, sorts recursively, and merges (O(n log n)).
    - Quick Sort: Picks a pivot, partitions the array, and sorts recursively (O(n log n) average, O(n²) worst).
    - Heap Sort: Uses a heap data structure to sort (O(n log n)).
- **Non-Comparison-Based Sorting**:
    - Counting Sort: Counts occurrences of elements for sorting (O(n+k), where k is the range of values).
    - Radix Sort: Sorts by processing individual digits (O(nk), where k is the number of digits).
    - Bucket Sort: Distributes elements into buckets and sorts each bucket (O(n+k) average).

### 2. **Searching Algorithms**

Algorithms to find an element in a data structure.

- Linear Search: Checks each element sequentially (O(n)).
- Binary Search: Searches sorted arrays by halving the search space (O(log n)).
- Jump Search: Jumps ahead by fixed steps in a sorted array (O(√n)).
- Interpolation Search: Estimates position based on value distribution in sorted arrays (O(log log n) average, O(n) worst).
- Exponential Search: Combines binary search with range doubling for sorted arrays (O(log n)).
- Hash-based Search: Uses a hash table for O(1) average-case lookup.

### 3. **Graph Algorithms**

Algorithms for problems on graphs (nodes and edges).

- **Traversal/Search**:
    - Depth-First Search (DFS): Explores as far as possible along each branch (O(V+E)).
    - Breadth-First Search (BFS): Explores level by level (O(V+E)).
- **Shortest Path**:
    - [Dijkstra’s Algorithm: Finds shortest paths from a source in weighted graphs with non-negative weights (O((V+E) log V) with a priority queue)](obsidian://open?vault=ThanhDinh&file=Algorithm%2FAlgorithms%2FDijkstra's%20Algorithm).
    - Bellman-Ford Algorithm: Handles negative weights for shortest paths (O(VE)).
    - A* Search: Uses heuristics for shortest path in weighted graphs (O(E log V) with good heuristics).
    - Floyd-Warshall Algorithm: Finds all-pairs shortest paths (O(V³)).
- **Minimum Spanning Tree**:
    - Kruskal’s Algorithm: Builds a minimum spanning tree by adding edges in increasing weight (O(E log V)).
    - Prim’s Algorithm: Grows a minimum spanning tree from a starting node (O(V log V) with a priority queue).
- **Topological Sorting**:
    - DFS-based Topological Sort: Orders vertices in a directed acyclic graph (O(V+E)).
    - Kahn’s Algorithm: Uses in-degree for topological sorting (O(V+E)).
- **Network Flow**:
    - Ford-Fulkerson Algorithm: Computes maximum flow in a flow network (O(E * |f|) where |f| is the maximum flow).
    - Edmonds-Karp Algorithm: BFS-based max flow (O(VE²)).
- **Connected Components**:
    - Kosaraju’s Algorithm: Finds strongly connected components in directed graphs (O(V+E)).
    - Tarjan’s Algorithm: Finds strongly connected components in a single pass (O(V+E)).

### 4. **String Matching Algorithms**

Algorithms to find occurrences of a pattern in a text.

- Naive String Matching: Checks each position for a match (O(n*m)).
- [Knuth-Morris-Pratt (KMP): Uses a failure function to skip redundant checks (O(n+m)).](obsidian://open?vault=ThanhDinh&file=LeetCode%2FEasy%2FFind%20the%20Index%20of%20the%20First%20Occurrence%20in%20a%20String%2FSolutions%2FKMP%20(Knuth-Morris-Pratt)%20Algorithm%20for%20Substring%20Search)
- Boyer-Moore: Skips sections of text based on mismatch patterns (O(n+m) average, O(nm) worst).
- Rabin-Karp: Uses hashing for pattern matching (O(n+m) average, O(nm) worst).
- Aho-Corasick: Matches multiple patterns simultaneously (O(n+m+k), where k is output size).
- Suffix Tree/Array Algorithms: Used for complex string operations (e.g., longest common substring, O(n)).

### 5. **Dynamic Programming Algorithms**

Algorithms that solve problems by breaking them into overlapping subproblems.

- Fibonacci Sequence: Computes nth Fibonacci number (O(n) with memoization).
- Knapsack Problem (0/1 and Fractional): Optimizes value within weight constraints (O(nW) for 0/1, O(n log n) for fractional).
- Longest Common Subsequence (LCS): Finds the longest subsequence common to two strings (O(mn)).
- Longest Increasing Subsequence (LIS): Finds the longest increasing subsequence in an array (O(n log n) with optimization).
- Matrix Chain Multiplication: Optimizes the order of matrix multiplications (O(n³)).
- Edit Distance (Levenshtein): Computes minimum edits to transform one string into another (O(mn)).
- Subset Sum: Determines if a subset sums to a target (O(n*sum)).
- Traveling Salesman Problem (Dynamic): Finds the shortest tour visiting all cities (O(n² * 2ⁿ)).

### 6. **Greedy Algorithms**

Algorithms that make locally optimal choices to achieve a global solution.

- Activity Selection: Selects maximum non-overlapping activities (O(n log n)).
- Huffman Coding: Builds optimal prefix codes for compression (O(n log n)).
- Fractional Knapsack: Maximizes value in a knapsack with fractional items (O(n log n)).
- Dijkstra’s Algorithm (also greedy): Shortest path in non-negative weighted graphs.
- Kruskal’s and Prim’s Algorithms (also greedy): Minimum spanning tree algorithms.

### 7. **Divide and Conquer Algorithms**

Algorithms that divide a problem into smaller subproblems and combine solutions.

- Merge Sort: Divides and merges sorted subarrays.
- Quick Sort: Partitions and recursively sorts.
- Binary Search: Divides sorted array to search.
- Strassen’s Matrix Multiplication: Optimizes matrix multiplication (O(n^2.807)).
- Closest Pair of Points: Finds the closest pair in a set of points (O(n log n)).

### 8. **Backtracking Algorithms**

Algorithms that explore all possibilities to find solutions.

- N-Queens Problem: Places N queens on an NxN chessboard without conflicts (O(n!)).
- Subset Sum: Finds subsets summing to a target (O(2ⁿ)).
- Graph Coloring: Assigns colors to graph vertices without adjacent conflicts (O(kⁿ), where k is the number of colors).
- Sudoku Solver: Solves a Sudoku puzzle (O(9^m), where m is empty cells).
- Hamiltonian Cycle: Finds a cycle visiting all vertices exactly once (O(n!)).

### 9. **Randomized Algorithms**

Algorithms that use randomness to simplify or approximate solutions.

- Quick Sort (Randomized Pivot): Reduces worst-case probability (O(n log n) expected).
- Monte Carlo Algorithms: Approximate solutions with probabilistic guarantees (e.g., primality testing).
- Las Vegas Algorithms: Guarantee correctness but vary in runtime (e.g., randomized quicksort).
- Karger’s Algorithm: Finds minimum cut in a graph (O(n² log n) expected).
- Randomized Primality Testing (Miller-Rabin): Tests if a number is prime (O(k log n) for k iterations).

### 10. **Approximation Algorithms**

Algorithms for NP-hard problems that provide near-optimal solutions.

- Vertex Cover: Approximates minimum vertex cover (2-approximation).
- Traveling Salesman Problem (Metric): Christofides algorithm for metric TSP (1.5-approximation).
- Set Cover: Greedy approach for set cover (log n-approximation).
- Knapsack: Greedy or dynamic programming-based approximations.

### 11. **Geometric Algorithms**

Algorithms for computational geometry problems.

- Convex Hull (Graham’s Scan, Jarvis March): Finds the smallest convex polygon enclosing points (O(n log n) for Graham’s).
- Line Segment Intersection: Detects intersections among line segments (O(n log n)).
- Closest Pair of Points: Finds the closest pair in a plane (O(n log n)).
- Sweep Line Algorithms: Solves geometric problems by sweeping a line (e.g., area of union of rectangles).

### 12. **Mathematical Algorithms**

Algorithms for numerical and mathematical computations.

- Euclidean GCD: Computes greatest common divisor (O(log min(a,b))).
- Fast Fourier Transform (FFT): Computes discrete Fourier transform (O(n log n)).
- Primality Testing (Miller-Rabin, AKS): Tests if a number is prime.
- Modular Exponentiation: Computes large powers efficiently (O(log n)).
- Sieve of Eratosthenes: Finds all primes up to n (O(n log log n)).

### 13. **Data Compression Algorithms**

Algorithms for reducing data size.

- Huffman Coding: Variable-length prefix codes (O(n log n)).
- Run-Length Encoding: Compresses repeated sequences (O(n)).
- Lempel-Ziv-Welch (LZW): Dictionary-based compression (O(n)).
- Burrows-Wheeler Transform: Used in bzip2 for text compression.

### 14. **Cryptographic Algorithms**

Algorithms for security and encryption.

- RSA: Public-key encryption based on modular exponentiation.
- AES (Advanced Encryption Standard): Symmetric-key encryption.
- SHA (Secure Hash Algorithm): Hashing for data integrity.
- Diffie-Hellman Key Exchange: Establishes shared secrets over insecure channels.

### 15. **Machine Learning Algorithms**

Algorithms for data analysis and prediction (high-level overview).

- Linear Regression: Fits a linear model to data.
- K-Means Clustering: Partitions data into k clusters.
- Decision Trees: Hierarchical decision-making models.
- Support Vector Machines (SVM): Finds optimal hyperplanes for classification.
- Neural Network Backpropagation: Trains neural networks via gradient descent.
- Gradient Descent: Optimizes objective functions iteratively.

## 16. Data Structure Algorithms (Trees and Heaps)

Algorithms used to maintain, organize, and query hierarchical data structures efficiently.

- **Heaps (Priority Queues):** Used for fast $O(1)$ access to the min/max element and $O(\log n)$ insertion/deletion. Essential for algorithms like Prim's and Dijkstra's.
    
- **Binary Search Tree (BST):** Fundamental search structure (O($h$) where $h$ is height).
    
- **Trie (Prefix Tree):** Used for fast string search and auto-completion (O(length of key)).
    
- **Self-Balancing Binary Search Trees (In-Memory Optimization):**
    
    - [**Red-Black Tree:**](obsidian://open?vault=ThanhDinh&file=Algorithm%2FAlgorithms%2FRed-Black%20Tree) Maintains near-optimal balance using color properties, guaranteeing **$O(\log N)$** worst-case time for search, insertion, and deletion. Widely used in programming language standard libraries (`std::map`).
        
    - [**AVL Tree:**](obsidian://open?vault=ThanhDinh&file=Algorithm%2FAlgorithms%2FAVL%20Tree) The first self-balancing BST. Maintains the strictest balance (height difference $\le 1$), offering the fastest **search** time but requiring more rotation overhead than RBTs upon updates.
        
    - [**Splay Tree:**](obsidian://open?vault=ThanhDinh&file=Algorithm%2FAlgorithms%2FSplay%20Tree) Self-adjusting tree that moves the most recently accessed node to the root. Excellent for data with **uneven access patterns** (caching), guaranteeing **$O(\log N)$ amortized** time.
        
- **External Memory Trees (Disk Optimization):**
    
    - [**B-Tree:**](obsidian://open?vault=ThanhDinh&file=Algorithm%2FAlgorithms%2FB-Tree) M-way search tree optimized for disk-based storage. Its wide, shallow structure minimizes **Disk I/O** (disk block reads) for database indexing and file systems ($O(\log_M N)$ where $M$ is large).
        
    - [**B+ Tree:**](obsidian://open?vault=ThanhDinh&file=Algorithm%2FAlgorithms%2FB%2B%20Tree) Variation of the B-Tree where all data is stored only in the **leaf nodes**, and the leaves are linked sequentially. Ideal for extremely fast **range queries** in database systems.