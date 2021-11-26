# Solution 1 Union Find

### Approach

Using **Union Find **to find the number of unconnected components

```java
class Solution {
    int countConnectedComponent;
    int[] parent;
    
    public int makeConnected(int n, int[][] connections) {
        if (connections.length < n - 1) return -1;
        countConnectedComponent = n;
        parent = new int[n];
        for(int i = 0; i < n; i++) {
            parent[i] = i;
        }
        for(int[] c : connections) {
            union(c[0], c[1]);
        }
        return countConnectedComponent - 1;
    }
    
    public int findRoot(int p) {
        if (p == parent[p]) return p;
        parent[p] = findRoot(parent[p]);
        return parent[p];
    }
    public void union(int p, int q) {
        int rootP = findRoot(p);
        int rootQ = findRoot(q);
        if (rootP != rootQ) {
            parent[rootP] = rootQ;
            countConnectedComponent--;
        }
    }
}
```
