# Solution 1 Union Find

### Approach

Using **UnionFind**. The only special tricky part is the "node" is 2D.

```java
class Solution {
    List<Integer> answer;
    int parent[][][];
    int grid[][];
    public List<Integer> numIslands2(int m, int n, int[][] positions) {
        grid = new int[m][n];
        int[] tempAnswer = new int[positions.length + 1];
        tempAnswer[0] = 0;
        answer = new ArrayList<>();
        parent = new int[m][n][2];
        for(int i = 0; i < m; i++) {
            for(int j = 0; j < n; j++) {
                parent[i][j][0] = i;
                parent[i][j][1] = j;
            }
        }
        for(int i = 0; i < positions.length; i++) {
            int lastAnswer = tempAnswer[i] + 1;
            int[] p = positions[i];
            if (grid[p[0]][p[1]] == 1) {
                tempAnswer[i+1] = lastAnswer - 1;
                continue;
            }
            grid[p[0]][p[1]] = 1;
            List<int[]> neighbors = getPotential(p, m, n);
            
            for (int j = 0; j < neighbors.size(); j++) {
                if (union(p, neighbors.get(j))) {
                    lastAnswer--;
                }
            }
            tempAnswer[i+1] = lastAnswer;
        }
        for(int i = 1; i < tempAnswer.length; i++) {
            answer.add(tempAnswer[i]);
        }
        return answer;
    }
        
    public int[] findRoot(int j, int k) {
        if (parent[j][k][0] == j && parent[j][k][1] == k) return new int[]{j, k};
        parent[j][k] = findRoot(parent[j][k][0], parent[j][k][1]);
        return parent[j][k];
    }
    public boolean union(int[] p, int[] q) {
        int[] rootP = findRoot(p[0], p[1]);
        int[] rootQ = findRoot(q[0], q[1]);
        if (rootP[0] != rootQ[0] || rootP[1] != rootQ[1]) {
            parent[rootP[0]][rootP[1]] = rootQ;
            return true;
        }
        return false;
    }
    public List<int[]> getPotential(int[] p, int m, int n) {
        List<int[]> ret = new ArrayList<>();
        if (p[0] - 1 >= 0 && grid[p[0] - 1][p[1]] == 1) ret.add(new int[] {p[0] - 1, p[1]});
        if (p[0] + 1 < m && grid[p[0] + 1][p[1]] == 1) ret.add(new int[] {p[0] + 1, p[1]});
        if (p[1] - 1 >= 0 && grid[p[0]][p[1] - 1] == 1) ret.add(new int[] {p[0], p[1] - 1});
        if (p[1] + 1 < n && grid[p[0]][p[1] + 1] == 1) ret.add(new int[] {p[0], p[1] + 1});
        return ret;
    }
}
```

```java
class Solution {   
  class UnionFind {
    int count; // # of connected components
    int[] parent;
    int[] rank;

    public UnionFind(char[][] grid) { // for problem 200
      count = 0;
      int m = grid.length;
      int n = grid[0].length;
      parent = new int[m * n];
      rank = new int[m * n];
      for (int i = 0; i < m; ++i) {
        for (int j = 0; j < n; ++j) {
          if (grid[i][j] == '1') {
            parent[i * n + j] = i * n + j;
            ++count;
          }
          rank[i * n + j] = 0;
        }
      }
    }

    public UnionFind(int N) { // for problem 305 and others
      count = 0;
      parent = new int[N];
      rank = new int[N];
      for (int i = 0; i < N; ++i) {
        parent[i] = -1;
        rank[i] = 0;
      }
    }

    public boolean isValid(int i) { // for problem 305
      return parent[i] >= 0;
    }

    public void setParent(int i) {
      parent[i] = i;
      ++count;
    }

    public int find(int i) { // path compression
      if (parent[i] != i) parent[i] = find(parent[i]);
      return parent[i];
    }

    public void union(int x, int y) { // union with rank
      int rootx = find(x);
      int rooty = find(y);
      if (rootx != rooty) {
        if (rank[rootx] > rank[rooty]) {
          parent[rooty] = rootx;
        } else if (rank[rootx] < rank[rooty]) {
          parent[rootx] = rooty;
        } else {
          parent[rooty] = rootx; rank[rootx] += 1;
        }
        --count;
      }
    }

    public int getCount() {
      return count;
    }
  }

  public List<Integer> numIslands2(int m, int n, int[][] positions) {
    List<Integer> ans = new ArrayList<>();
    UnionFind uf = new UnionFind(m * n);

    for (int[] pos : positions) {
      int r = pos[0], c = pos[1];
      List<Integer> overlap = new ArrayList<>();

      if (r - 1 >= 0 && uf.isValid((r-1) * n + c)) overlap.add((r-1) * n + c);
      if (r + 1 < m && uf.isValid((r+1) * n + c)) overlap.add((r+1) * n + c);
      if (c - 1 >= 0 && uf.isValid(r * n + c - 1)) overlap.add(r * n + c - 1);
      if (c + 1 < n && uf.isValid(r * n + c + 1)) overlap.add(r * n + c + 1);

      int index = r * n + c;
      uf.setParent(index);
      for (int i : overlap) uf.union(i, index);
      ans.add(uf.getCount());
    }

    return ans;
  }
}
```

### Analysis

* Time complexity : O(m×n+L) where L is the number of operations, m is the number of rows and n is the number of columns. it takes O(m×n) to initialize UnionFind, and O(L) to process positions. Note that Union operation takes essentially constant time[\[1\]](https://leetcode.com/problems/number-of-islands-ii/solution/#fn1) when UnionFind is implemented with both path compression and union by rank.
* Space complexity : O(m×n) as required by UnionFind data structure.

\
