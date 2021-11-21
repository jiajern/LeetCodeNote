# Solution 1

### Approach

DFS travel the graph and check for loop and return whether all nodes are visited.

```java
class Solution {
    public boolean validTree(int n, int[][] edges) {
        List<List<Integer>> adjacencyList = new ArrayList<>();
        for(int i = 0; i < n; i++) {
            adjacencyList.add(new ArrayList<>());
        }
        for(int[] edge : edges) {
            adjacencyList.get(edge[0]).add(edge[1]);
            adjacencyList.get(edge[1]).add(edge[0]);
        }
        Map<Integer, Integer> parent = new HashMap<>();
        parent.put(0, -1);
        Stack<Integer> stack = new Stack<>();
        stack.push(0);
        
        while(!stack.isEmpty()) {
            int node = stack.pop();
            for(int neighbor : adjacencyList.get(node)) {
                if (neighbor == parent.get(node)) continue;
                if (parent.containsKey(neighbor)) return false; // means we have reached the neighbor node via other path, this create loop
                stack.push(neighbor);
                parent.put(neighbor, node);
            }
        }
        return parent.size() == n;
    }
}
```

### Take Away

* Ways to represent a graph:
  * Adjacency List
  * Adjacency Matrix
  * Linked Representation
