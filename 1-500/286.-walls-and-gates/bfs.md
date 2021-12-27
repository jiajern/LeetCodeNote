# BFS

### Approach

Find all gate and expand from the gates

```java
class Solution {
    public int INF = Integer.MAX_VALUE;
    public int GATE = 0;
    public int WALL = -1;
    public void wallsAndGates(int[][] rooms) {
        int R = rooms.length, C = rooms[0].length;
        Deque<Integer> deque = new ArrayDeque<>();
        for (int r = 0; r < R; r++) {
            for (int c = 0; c < C; c++) {
                if (rooms[r][c] == GATE) deque.addLast(C * r + c);
            }
        }
        while (!deque.isEmpty()) {
            int coordinate = deque.removeFirst();
            int r = coordinate / C;
            int c = coordinate % C;
            if (r > 0 && rooms[r-1][c] == INF) {
                rooms[r-1][c] = rooms[r][c] + 1;
                deque.addLast(C * (r-1) + c);
            }
            if (r < R-1 && rooms[r+1][c] == INF) {
                rooms[r+1][c] = rooms[r][c] + 1;
                deque.addLast(C * (r+1) + c);
            }
            if (c > 0 && rooms[r][c-1] == INF) {
                rooms[r][c-1] = rooms[r][c] + 1;
                deque.addLast(C * r + c-1);
            }
            if (c < C-1 && rooms[r][c+1] == INF) {
                rooms[r][c+1] = rooms[r][c] + 1;
                deque.addLast(C * r + c+1);
            }
        }
    }
}
```
