# Data Structures - Concepts & Terminology

## _call stack_
- a data structure that stores information about the active subroutines (or function calls) of a computer program. 
- used by most programming languages to keep track of function calls and local variables
- each time a function is called, a new frame (or record) is added to the stack containing information such as the function's parameters, its local variables, and the address to return control to once the function completes

## _B-Trees (Balanced Trees)_
-  a type of data structure used extensively in databases and filesystems to organize and manage large amounts of sorted data efficiently (ie: SQL dbs)
-  B-Trees play a crucial role in indexing, which significantly speeds up data retrieval operations

### Key Characteristics of B-Trees:

**Balanced Tree Structure:** B-Trees are balanced, meaning the path from the root to any leaf is the same length, ensuring efficient data operations (insertion, deletion, search) that are logarithmic in time complexity `O(log n)`.

**Nodes with Multiple Keys:** Each node in a B-Tree can hold multiple keys (and corresponding data pointers), unlike binary search trees where each node holds a single key. This feature allows B-Trees to remain shallow while storing large amounts of data, leading to fewer disk accesses during operations.

**Sorted Order:** The keys within nodes are stored in a sorted order, and each node’s keys act as separation values which divide its subtrees. For any given node, all keys in the left subtree are less than the node’s key, and all keys in the right subtree are greater.

**Variable Node Capacity:** B-Trees are parameterized by the order (or degree) which defines the maximum and minimum number of keys a node can hold. This adaptability makes B-Trees very efficient in terms of balancing the tree and optimizing storage.

**Efficient Disk Accesses:** B-Trees are designed to minimize disk accesses, making them ideal for storage systems where data access time is predominantly determined by disk seek time. Their structure is optimized for systems that read and write large blocks of data.
