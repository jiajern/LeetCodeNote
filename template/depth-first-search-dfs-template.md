# Depth First Search DFS Template

Template for DFS iterative

```java
// Use a stack to keep track of unexplored nodes.
Stack<Integer> stack = new Stack<>();
stack.push(0);
// Use a set to keep track of already seen nodes to
// avoid infinite looping. 
Set<Integer> seen = new HashSet<>();
seen.add(0);

// While there are nodes remaining on the stack...
while (!stack.isEmpty()) {
    int node = stack.pop(); // Take one off to visit.
    // Check for unseen neighbours of this node:
    for (int neighbour : adjacencyList.get(node)) {
        if (seen.contains(neighbour)) {
            continue; // Already seen this node.
        }
        // Otherwise, put this neighbour onto stack
        // and record that it has been seen.
        stack.push(neighbour);
        seen.add(neighbour);
    }
}
```
