# Solution 1

### Approach

Using **UnionFind**, each union we did, meaning the connected component will decrease by 1

```java
class Solution {
    int count;
    int[] parent;
    public int countComponents(int n, int[][] edges) {
        count = n;
        parent = new int[n];
        for(int i = 0; i < n; i++) {
            parent[i] = i;
        }
        for(int[] edge : edges) {
            union(edge[0], edge[1]);
        }
        return count;
    }
    public int findRoot(int p) {
        if(p == parent[p]) return p;
        else return findRoot(parent[p]);
    }
    public boolean union(int p, int q) {
        int rootP = findRoot(p);
        int rootQ = findRoot(q);
        if (rootP != rootQ) {
            parent[rootP] = rootQ;
            count--;
            return true;
        }
        return false;
    }
}
```
