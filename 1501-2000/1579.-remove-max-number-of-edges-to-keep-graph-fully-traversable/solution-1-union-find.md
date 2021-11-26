# Solution 1 Union Find

### Approach

Using **UnionFind** to connect the node. If the edge can be used than we increment the count. At the end return how many edge we have minus how many we have been used

```java
class Solution {
    class UnionFind {
        int[] components;
        int distinctComponents;
        public UnionFind(int n) {
            distinctComponents = n;
            components = new int[n];
            for(int i = 0; i < n; i++) components[i] = i;
        }
        public int findRoot(int p) {
            if (components[p] == p) return p;
            components[p] = findRoot(components[p]);
            return components[p];
        }
        public boolean unite(int p, int q) {
            int rootP = findRoot(p);
            int rootQ = findRoot(q);
            if (rootP != rootQ) {
                components[rootP] = rootQ;
                distinctComponents--;
                return true;
            }
            return false;
        }
        public boolean united() {
            return distinctComponents == 1;
        }
    }
    public int maxNumEdgesToRemove(int n, int[][] edges) {
        Arrays.sort(edges, (a, b) -> b[0] - a[0]);
        
        UnionFind alice = new UnionFind(n);
        UnionFind bob = new UnionFind(n);
        
        int edgeUsed = 0;
        
        for(int[] e : edges) {
            int type = e[0], a = e[1] - 1, b = e[2] - 1;
            switch(type) {
                case 3:
                    if (alice.unite(a, b) | bob.unite(a, b)) edgeUsed++;
                    break;
                case 2:
                    if (bob.unite(a, b)) edgeUsed++;
                    break;
                case 1:
                    if (alice.unite(a, b)) edgeUsed++;
                    break;
            }
        }
        return alice.united() && bob.united() ? edges.length - edgeUsed : -1;
    }
}
```
