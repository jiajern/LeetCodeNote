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
