# Binary Tree

![Binary_tree_v2 svg](https://github.com/bobbygrdn/developer-notebook/assets/96712943/03451ddf-de5b-4ba0-bdf2-e212df916040)

## Rules of BT

- Tree has only 1 root node
- Tree has only 1 path to each node
- Tree has maximum 2 nodes attached to each node

## Time and Space Complexity

|| Time Complexity | Space Complexity |
|:---:|:---:|:---:|
| Insertion | O(N) | O(N^0.5) |
| Search | O(N) | O(N^0.5) |
| Deletion | O(N) | O(N^0.5) |

## Search Algorithms

### Breadth First Search - Iterative

```
// Create an empty queue using an array
// Shift the root node into the queue

/* Loop through the Tree using a while loop with the condition of checking 
 * to see if the queue is empty. Create a temporary variable to hold the 
 * current node and assign it to the next node in the queue using the shift 
 * method.
 */

// Perform some action on the value of the current node

// Check to see if the left node is null
// If it is not null, push the left node into the queue

// Check to see if the right node is null
// If it is not null, push the right node into the queue
```

### Depth First Search - Iterative

// Create an empty stack using an array
// Push the root node into the stack

/* Loop through the Tree using a while loop with the condition of checking 
 * to see if the stack is empty. Create a temporary variable to hold the 
 * current node and assign it to the next node in the stack using the pop 
 * method.
 */

// Perform some action on the value of the current node

// Check to see if the left node is null
// If it is not null, push the left node onto the stack

// Check to see if the right node is null
// If it is not null, push the right node onto the stack
