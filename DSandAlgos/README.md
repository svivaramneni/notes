* Data structures can be neatly classified as either contiguous or linked, depending upon whether they are based on arrays or pointers.
* **Contiguous**: Arrays, Matrices, Heaps, Hash tables
* **Linked DS**: lists, trees, graphs

* Big-O notation gives an upper bound of the complexity in the worst case.
	* Constant time – O(1)
	* Logarithmic time: O(log(n))
	* Linear Time: O(n)
	* Linearithmic Time: O(nlog(n))
	* Quadric Time: O(n^2)
	* Cubic Time: O(n^3)
	* Factorial Time: O(n!)
	
### Arrays
* Array has length field, Collections has size() method and String has length() method.
* Static array is a fixed length container containing n elements. Contiguous memory addresses.
* Dynamic arrays double in size and copy the contents from previous array. Time complexity O(n)
* Dynamic arrays can grow and shrink in size as needed. `Ex: ArrayList`
* Instead of deleting an entry, consider overwriting it.

#### Advantages of Arrays:
* Constant-time access given the index
* Space efficiency: No wasted space for pointers
* Memory locality: iterating is fast.
#### Downsides
* We cannot adjust their size in the middle.

### Linked List
* Insertion O (1) – At beginning or end. By default, most people assume insertion means, adding at the end.
* Deletion or Searching – O(n)
* Unlike arrays, list is dynamically resized.
* Not good for random insertion, accessing nodes by index and searching.
* Used in List, Queue & Stack.
* Always maintain a reference to the Head and Tail
* Singly LinkedList uses less memory, simpler Implementation and cannot easily access previous elements.
* Doubly LinkedList	can be traversed backwards, takes 2X memory.
* Remove node from singly linked can be done easily with 2 pointers.

#### Advantages of Linked lists over arrays
* Overflow of LL never occurs unless memory is full.
* Insertion and deletions are simpler.
#### Downsides
* LL require extra space for storing pointer fields.
* LL do not allow efficient random access.
* Arrays allow better memory locality and cache performance.

* Stack and Queue can be implemented using either arrays or linked lists. Key is whether we know upper bound on the size upfront.

### Binary Search Tree
* Some DS allow fast search or flexible update, but not fast search “and” flexible update.
* Binary tree nodes have left, right pointer fields, (optional) parent pointer and a data field.
* Binary search tree runs in O(h) time, where h denotes the height of the tree.
* Left subtree of root node x, contains nodes whose values < x and right subtree contains nodes whose values are >= x. Each node follows same rule.
```
			23
		14		31
	7		17
		9

Ex: Unbalanced binary search tree
```
* Deleting an element from BST involves 4 combinations. Deleting leaf node, deleting node with left child, deleting node with right child and deleting a node with left and right child. We need reference to the parent to do this. Implement this.

### Traversal
* PreOrder Traversal: root, left, right
* Postorder: left, right, root
* Inorder: left, root, right
* Insertion, deletion, lookup is O(logn) for a reasonably balanced binary tree.

### Heap
* Simple tree data structure with 2 variants/strategies. Min heap, max heap. 
* Min Heap: Each parent node would have a value that is <= its children. So smallest element is at the root.
* Unlike other tree DS’s, Heap is generally implemented as an array.
	* Parent Index: (index-1)/2
	* Left child: 2*index+1
	* Right child: 2*index+2
* Inserting an element into heap involves 2 steps. 
	* Keep track of the next free index through counter. Insert and increment counter. O(1).
	* Validate order and keep sorting value with parent. O(logn).

### AVL trees: 
Binary search tree with a self-balancing condition such that the diff between left and right subtrees is no more than 1.
* Height of AVL tree is O(logn).
* Tree rotation is a constant time operation. 
* Both left and right tree rotation preserves standard BST properties and decrease the height. 
* AVL insertion is similar to BST, then apply rebalancing when necessary.

### Sorting and Searching
* Both quick sort and merge sort runtime is O(nlogn)
* Recursion should only be applied to fast algorithms. i.e. < n^2.
* Using recursion for a LL, probably a little overkill.
* Heaps are well-suited for algorithms that merge sorted data streams.
* Heap sorting: Fast sorting via data structures.
* Heaps support efficient priority queue.  They maintain partial order (Weaker than sorted, stronger than random order)
* Heap enables binary trees without using any pointers. Data is stored as array of keys, and position of keys to implicitly satisfy the role of the pointers. Root of the tree in first position of the array, and its left and right children in second and third positions respectively. 
* This implicit representation of binary trees saves memory but is less flexible than using pointers. We cannot store arbitrary tree topologies with wasting large amount of space. We cannot move subtrees around easily.

#### Merge Sort: Classic divide and conquer.
* It’s great for sorting linked lists, because it doesn’t rely on random access.
* Its primary disadvantage is the need for auxiliary buffer for arrays.

#### Quicksort
* Properly implemented quicksort is faster than mergesort or heapsort. Key here is to select good pivot and partition.

#### Distribution sort: Sorting via Bucketing
* Bucketing is very effective idea whenever we are confident that the distribution of data will be roughly uniform.
* Performance could be terrible, when the data distribution is not what we expected.

## Stack
* Usually implemented with Array or Linked Lists. Java comes with LL.

### Queue
* Queue is a linear DS which models real world queues by having two operations.
* Ex: Web server request management where you want FIFS, BFS
* Normal queues have constant insert and deletion times.
* Priority queues can be implemented with heaps. So that, minimum element could be at the top.
* Searching in queues is not common O(n)

### Priority Queues
* PQ is an abstract data type. Similar to normal queue except that each element has certain priority.
* PQ’s only support data that is comparable between elements.
* Heap: Heap is a tree-based DS that satisfies the heap invariant. If A is a parent node of B then A is ordered with respect to B for all nodes A, B in the heap.
```
				0                           8
	       7        6			       2        3
	   3     2    5	  4             5   6    4
       Max Heap                        Min Heap
```
* Heap should not have a cycle.
* PQs are used in shortest path algorithms.
* Breadth First Search algorithms to continuously grab the next most promising node.
* PQs are used in Graph Theory Algorithms.
* Complexity of PQ with binary heap
* Binary Heap Construction	O(n)
* Polling	O(log(n)
* Peeking	O(1)
* Adding	O(log(n))
* Priority Queue with binary heap where every node has 2 children except the last level.
* While inserting an element, we insert at the next logical leaf node, and keep swapping with the parent until the invariant is met (Bubbling up).
* Removing element from binary heap: with poll, we remove the root node first, then move last element to the root and keep bubbling down.
* While removing specific element, we search for the node first, then swap it with last element in the array and keep swapping until the invariant is met.

### Trees: 
* Tree is an undirected graph which satisfies following
	* An acyclic connected graph.
	* A connected graph with N nodes and N-1 edges.
	* A graph in which any two vertices are connected by exactly one path.

### Binary Tree
* A binary tree is a tree for which every node has at most two child nodes.

### Binary Search Tree
* It’s a binary tree that satisfies the BST invariant. i.e. left subtree has smaller elements and right subtree has larger elements.
* Complexity of BST’s
```
Operation	Average	Worst
Insert	O(log(n))	O(n)
Delete	O(log(n))	O(n)
Remove	O(log(n))	O(n)
Search	O(log(n))	O(n)
```
* While inserting/searching we always start at the root and there is no swapping.
* If we insert sorted elements in order (ex:1,2,3,4,5,6) then complexity could be linear.  
* Removing a node contains 2 steps. Find and remove. There are 4 type of node removals.

### Tree Traversals
* Pre-order prints before the recursive calls.
* In-order prints between the recursive calls.
* Post-order prints after the recursive calls.
* Level order traversal uses a queue. Similar to BFS. No recursion.

### Suffix Array
* Suffix array is an array which contains all the sorted suffixes of a string.

### Balanced Binary Search Tree
* Balanced Binary Search Tree is a self-balancing binary search tree. This type of tree will adjust itself in order to maintain a low (logarithmic) height allowing for faster operations such as insertions and deletions.
* Worst case complexity for all operations is O(log(n))
* Tree is rotated to satisfy the invariant.

### Graph Theory
* Undirected graph edges have no orientation.
* Directed graph in which edges have orientation.
* Tree is undirected graph with no cycles.
* Directed Acyclic Graphs are directed graph with no cycles. All out-trees are DAGs but not all DAGs are out-trees.

### Adjacency Matrix
* It is a very simple way to represent a graph. The idea is that the cell m[i][j] represents the edge weight of going from node i to node j.
* Space efficient for representing dense graphs	Requires O(V^2) space
* Edge weight lookup is O (1), Iterating over all edges takes O(V^2) time
* Simplest graph representation	

### Adjacency List
* An adjacency list is a way to represent a graph as a map from nodes to lists of edges. Ex: C- > [(A, 4), (B, 1), (D,2)]
* Space efficient for representing sparse graphs	Less space efficient for denser graphs.
* Iterating over all edges is efficient, Edge weight lookup is O(E). Slightly more complex graph representation

### Edge List
* It is a way to represent a graph simply as an unordered list of edges. 
`Ex: [(C, A, 4), (A, C,1) …...]`
* It is seldomly used because of lack of structure.

### Depth First Search Algorithm
* It is the most fundamental search algorithm used to explore nodes and edges of a graph.
* Time complexity O(V+E).
* Visits a node, then visits one of its neighbors and so on, until it reaches back to the same node. Then back tracks to the last visited node and takes another path.

### Breadth First Search Algorithm
* It is the most fundamental search algorithm used to explore nodes and edges of a graph.
* Time complexity O(V+E)
* Useful in finding shortest path in unweighted graph.
* Visits a node and all its neighbors and moves onto to next neighbor.
* It uses a Queue DS to track which node to visit next.

### Dijkstra’s Algorithm for finding shortest path
* It is a single source shortest path algorithm for graphs with non-negative edge weights.
* It uses indexed priority queue.

### Dynamic Programming
* It is a technique for efficiently implementing a recursive algorithm by storing partial results.
* It is a tradeoff of space for time.























