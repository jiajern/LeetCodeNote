# Union Find

```java
int countConnectedComponent = numberOfNode;
int[] parent = new int[numberOfNode];

public void main() {
    // initialize parent
    for(int i = 0; i < numberOfNode; i++) {
        parent[i] = i;
    }

    for(int[] edge : edges) {
        union(edge[0], edge[1]);
    }
}

// find the root for node p recursively
public int findRoot(int p) {
    if (p == parent[p]) return p;
    else return findRoot(parent[p]);
}

// union two nodes together
public void union(int p, int q) {
    int rootP = findRoot(p);
    int rootQ = findRoot(q);
    if (rootP != rootQ) {
        countConnectedComponent--;
        parent[rootP] = rootQ;
    }
}
```

```java
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
```
