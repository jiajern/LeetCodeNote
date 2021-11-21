# Solution 2

### Approach

Using **graph theory** and **DFS**

```java
class Solution {
    List<List<Integer>> adjacencyList = new ArrayList<>();
    Set<Integer> seen = new HashSet<>();
    
    public boolean validTree(int n, int[][] edges) {
        if (edges.length != n - 1) return false;

        for(int i = 0; i < n; i++) {
            adjacencyList.add(new ArrayList<>());
        }
        for(int[] edge : edges) {
            adjacencyList.get(edge[0]).add(edge[1]);
            adjacencyList.get(edge[1]).add(edge[0]);
        }
        dfs(0);
        return seen.size() == n;
    }
    
    public void dfs(int node) {
        if (seen.contains(node)) return;
        seen.add(node);
        for(int neighbor : adjacencyList.get(node)) {
            dfs(neighbor);
        }
    }
}syn
```

### Take Away

* Graph theory:&#x20;
  * if edge < node - 1 then it cannot be fully connected
  * if edge > node - 1 then it must have cycle

### Analysis

#### Time Complexity

O(n) because we need to travel all the node

#### Space Complexity

O(n) because adjacency list store n edge now and the recursive stack is n
