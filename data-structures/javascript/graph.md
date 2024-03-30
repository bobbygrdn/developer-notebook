# Directed Graph

![Directed_graph](https://github.com/bobbygrdn/developer-notebook/assets/96712943/ed4570c7-2289-40ba-afc3-8f8893a12b8d)

## Rules of DG

- DG connects one node to another using an edge
- A node connected to another node is called a "Neighbor Node"

## Time and Space Complexity

|| Time Complexity | Space Complexity|
| :---: | :---: | :---: |
| Insert Vertex | O(1) | O(1) |
| Insert Edge | O(1) | O(1) |
| Search Vertex | O(V) | O(1) |
| Search Edge | O(V) | O(1) |
| Delete Vertex | O(V+E) | O(V+E) |
| Delete Edge | O(E) | O(1) |

## Traversal Algorithms

### Breadth First Traversal

```
// Create an queue using an array that contains the source node

/* Loop through the Tree using a while loop with the condition of checking 
 * to see if the queue is empty. Create a temporary variable to hold the 
 * current node and assign it to the next node in the queue using the shift 
 * method.
 */

// Perform some action on the value of the current node

/* Loop through the neighbors of the source node by keying into the object 
 * using the for of loop. Push each neighbor into the back of the queue.
 */

```

### Depth First Traversal - Iterative

// Create an empty stack using an array

// Push the source node into the stack

/* Loop through the Tree using a while loop with the condition of checking 
 * to see if the stack is empty. Create a temporary variable to hold the 
 * current source node and assign it to the next node in the stack using the
 * pop method.
 */

// Perform some action on the value of the current node

/* Loop through the neighbors of the source node by keying into the object 
 * using the for of loop. Push each neighbor onto the top of the stack.
 */

### Depth First Traversal - Recursive

**This method uses an explicit base case**

// Perform some action on the value of the source node

/* Loop through the neighbors of the source node by keying into the object 
 * using the for of loop. Call the Depth First Traversal on each neighbor    
 * node.
 */
