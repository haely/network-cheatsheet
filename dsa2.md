# DSA Cheatsheet

## Data Structures

### Arrays
- **Description:** Contiguous block of memory storing elements of the same type.
- **Use Cases:** Simple lists, lookup tables, implementing other data structures.
- **Interview Notes:** Fast random access (O(1)), fixed size (in static arrays), dynamic arrays overcome this.

### Linked Lists
- **Description:** Sequence of nodes, each pointing to the next.
- **Use Cases:** Dynamic memory allocation, implementing stacks, queues, and graphs.
- **Interview Notes:** Efficient insertion/deletion (O(1)), no random access (O(n)), variations: singly, doubly, circular.

### Stacks (LIFO)
- **Description:** Last-In-First-Out (LIFO) data structure.
- **Use Cases:** Function call stacks, expression evaluation, undo/redo mechanisms.
- **Interview Notes:** Push and pop operations are O(1).

### Queues (FIFO)
- **Description:** First-In-First-Out (FIFO) data structure.
- **Use Cases:** Breadth-first search (BFS), task scheduling, handling requests.
- **Interview Notes:** Enqueue and dequeue operations are O(1).

### Hash Tables (Dictionaries)
- **Description:** Key-value pairs with fast average-case lookup.
- **Use Cases:** Caching, symbol tables, implementing sets.
- **Interview Notes:** Average O(1) lookup, insertion, deletion; worst-case O(n) (collisions).

### Trees
- **Description:** Hierarchical data structure with nodes and edges.
- **Use Cases:** Representing hierarchical data, searching, sorting.
- **Interview Notes:** Different types (binary, balanced, etc.), traversal algorithms (inorder, preorder, postorder).

### Binary Trees
- **Description:** Each node has at most two children (left and right).
- **Use Cases:** Binary search trees, expression trees, decision trees.
- **Interview Notes:** Important variations: BST, AVL, Red-Black trees.

### Binary Search Trees (BST)
- **Description:** Ordered binary tree, left <= node < right.
- **Use Cases:** Efficient searching, sorting.
- **Interview Notes:** Search, insert, delete are O(log n) on average, O(n) in worst case (unbalanced).

### Heaps (Priority Queues)
- **Description:** Tree-based data structure satisfying heap property (min/max).
- **Use Cases:** Priority queues, heap sort, graph algorithms (Dijkstra).
- **Interview Notes:** Min-heap: smallest element at root; Max-heap: largest element at root.

### Graphs
- **Description:** Collection of nodes (vertices) and edges.
- **Use Cases:** Representing networks, social connections, maps.
- **Interview Notes:** Directed vs. undirected, weighted vs. unweighted, traversal algorithms (DFS, BFS).

## Algorithms

### Sorting

-   **Bubble Sort:** Simple, O(n^2).
-   **Insertion Sort:** Efficient for small lists, O(n^2).
-   **Selection Sort:** Simple, O(n^2).
-   **Merge Sort:** Divide and conquer, O(n log n).
-   **Quick Sort:** Divide and conquer, average O(n log n), worst O(n^2).
-   **Heap Sort:** Heap-based, O(n log n).

### Searching

-   **Linear Search:** O(n).
-   **Binary Search:** O(log n) (sorted arrays).

### Graph Algorithms

-   **Depth-First Search (DFS):** Traverses depth-first, uses stack or recursion.
    -   **Use Cases:** Path finding, cycle detection.
-   **Breadth-First Search (BFS):** Traverses level-by-level, uses queue.
    -   **Use Cases:** Shortest path in unweighted graphs, level order traversal.
-   **Dijkstra's Algorithm:** Shortest path in weighted graphs (non-negative weights).
-   **Bellman-Ford Algorithm:** Shortest path in weighted graphs (can handle negative weights).
-   **Floyd-Warshall Algorithm:** Shortest paths between all pairs of vertices.
-   **Topological Sort:** Linear ordering of vertices in a directed acyclic graph (DAG).
-   **Minimum Spanning Tree (MST):** Kruskal's, Prim's algorithms.

### Dynamic Programming (DP)

-   **Description:** Breaks down problems into overlapping subproblems, stores results to avoid redundant computations.
-   **Use Cases:** Optimization problems, Fibonacci sequence, knapsack problem.
-   **Interview Notes:** Identify overlapping subproblems, define state, define recurrence relation, memoization/tabulation.

### Recursion

-   **Description:** Function calls itself to solve smaller instances of the problem.
-   **Use Cases:** Tree traversals, divide and conquer algorithms.
-   **Interview Notes:** Base case, recursive case, stack overflow risk.

### Two Pointers

-   **Description:** Uses two pointers to iterate through a data structure.
-   **Use Cases:** Searching, sorting, finding pairs.
-   **Interview Notes:** Efficient for problems involving sorted arrays or linked lists.

### Sliding Window

-   **Description:** Maintains a window of elements and slides it through a data structure.
-   **Use Cases:** Finding subarrays or substrings with specific properties.
-   **Interview Notes:** Useful for optimization problems.

### Greedy Algorithms

-   **Description:** Makes locally optimal choices at each step to find a global optimum.
-   **Use Cases:** Activity selection, fractional knapsack.
-   **Interview Notes:** Not always guaranteed to find the optimal solution.

## Coding Patterns

-   **1D Array:** Linear traversal, two pointers, sliding window.
-   **2D Array/Matrix:** Nested loops, matrix traversal, dynamic programming.
-   **Trees:** Depth-first search (DFS), breadth-first search (BFS), recursion.
-   **Graphs:** DFS, BFS, Dijkstra's, topological sort.
-   **Dynamic Programming:** Memoization, tabulation, state transitions.
-   **Recursion:** Base case, recursive case, backtracking.
-   **Two Pointers:** Two pointers moving in opposite directions, or same direction with different speeds.
-   **Sliding Window:** Expand and shrink window based on conditions.
-   **Backtracking:** Explore all possible solutions by trying different choices.
-   **Divide and Conquer:** Break down a problem into smaller subproblems, solve recursively, and combine solutions.

## Tree/Graph Details

### Tree Types

-   **Binary Tree:** Each node has at most two children.
-   **Binary Search Tree (BST):** Ordered binary tree.
-   **AVL Tree:** Self-balancing BST.
-   **Red-Black Tree:** Self-balancing BST.
-   **Trie:** Tree-like data structure for efficient string prefix searching.
-   **Segment Tree:** Efficient range queries.
-   **Fenwick Tree (Binary Indexed Tree):** Efficient prefix sum queries.

### Graph Types

-   **Directed Graph:** Edges have direction.
-   **Undirected Graph:** Edges have no direction.
-   **Weighted Graph:** Edges have weights.
-   **Unweighted Graph:** Edges have no weights.
-   **Cyclic Graph:** Contains cycles.
-   **Acyclic Graph:** Contains no cycles.
-   **Directed Acyclic Graph (DAG):** Directed graph with no cycles.

### When to Use What

-   **BST:** Searching, sorting, ordered data.
-   **AVL/Red-Black Trees:** Balanced BSTs for frequent insertions/deletions.
-   **Trie:** String prefix searching, autocomplete.
-   **Segment/Fenwick Trees:** Range queries, prefix sums.
-   **DFS:** Path finding, cycle detection, exploring all paths.
-   **BFS:** Shortest path in unweighted graphs, level order traversal.
-   **Dijkstra's:** Shortest path in weighted graphs (non-negative weights).
-   **Topological Sort:** Scheduling tasks, dependency resolution.
-   **MST (Kruskal's/Prim's):** Finding minimum spanning trees in weighted graphs.
