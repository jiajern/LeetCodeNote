# BFS

### Approach

Using **BFS** expand from the side, find the overlap using "seen" hashset.

```java
class Solution {
    int R;
    int C;
    public List<List<Integer>> pacificAtlantic(int[][] heights) {
        List<List<Integer>> ret = new ArrayList<>();
        Set<Integer> po = new HashSet<>();
        Set<Integer> ao = new HashSet<>();
        Deque<Integer> poDeque = new ArrayDeque<>();
        Deque<Integer> aoDeque = new ArrayDeque<>();
        R = heights.length;
        C = heights[0].length;
        for (int r = 0; r < R; r++) {
            poDeque.addLast(r * C);
            po.add(r * C);
            aoDeque.addLast((r * C) + C-1);
            ao.add((r * C) + C-1);
        }
        for (int c = 0; c < C; c++) {
            poDeque.addLast(c);
            po.add(c);
            aoDeque.addLast((R-1) * C + c);
            ao.add((R-1) * C + c);
        }
        bfs(aoDeque, ao, heights);
        bfs(poDeque, po, heights);
        for(Integer i : ao) {
            if (po.contains(i)) {
                List<Integer> temp = new ArrayList<>();
                temp.add((int)i / C);
                temp.add((int)i % C);
                ret.add(temp);
            }
        }
        return ret;

    }
    public void bfs(Deque<Integer> deque, Set<Integer> seen, int[][] heights) {
        while(!deque.isEmpty()) {
            int coordinate = deque.removeFirst();
            int r = coordinate / C;
            int c = coordinate % C;
            int m = (r-1) * C + c; // up
            if (r > 0 && !seen.contains(m) && heights[r-1][c] >= heights[r][c]) {
                seen.add(m);
                deque.addLast(m);
            }
            int n = (r * C) + c-1; // left
            if (c > 0 && !seen.contains(n) && heights[r][c-1] >= heights[r][c]) {
                seen.add(n);
                deque.addLast(n);
            }
            int j = (r+1) * C + c; // down
            if (r < R-1 && !seen.contains(j) && heights[r+1][c] >= heights[r][c]) {
                seen.add(j);
                deque.addLast(j);
            }
            int k = (r * C) + c+1; // right
            if (c < C-1 && !seen.contains(k) && heights[r][c+1] >= heights[r][c]) {
                seen.add(k);
                deque.addLast(k);
            }
        }
    }
}
```
