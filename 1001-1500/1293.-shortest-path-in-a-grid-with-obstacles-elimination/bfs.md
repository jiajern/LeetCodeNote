# BFS

### Approach

Using BFS traverse the map. Treat every step as a state.

```java
class Solution {
    class StepState {
        public int steps, row, col, k;
        public StepState(int steps, int row, int col, int k) {
            this.steps = steps;
            this.row = row;
            this.col = col;
            this.k = k;
        }
        @Override
        public int hashCode() {
            return (this.row + 1) * (this.col + 1) * this.k;
        }
        @Override
        public boolean equals(Object other) {
            if (!(other instanceof StepState)) return false;
            StepState otherStepState = (StepState) other;
            return this.row == otherStepState.row &&
                this.col == otherStepState.col &&
                this.k == otherStepState.k;
        }
        @Override
        public String toString() {
            return String.format("%d %d %d", this.row, this.col, this.k);
        }
    }
    
    public int shortestPath(int[][] grid, int k) {
        int R = grid.length, C = grid[0].length;
        int[] target = {R-1, C-1};
        if (k >= R + C - 2) return R + C - 2;
        
        Deque<StepState> queue = new LinkedList<>();
        HashSet<StepState> seen = new HashSet<>();
        
        StepState start = new StepState(0, 0, 0, k);
        queue.addLast(start);
        seen.add(start);
        
        while (!queue.isEmpty()) {
            StepState curr = queue.pollFirst();
            if (target[0] == curr.row && target[1] == curr.col) return curr.steps;
            int[] nextSteps = {curr.row, curr.col+1,
                               curr.row+1, curr.col,
                               curr.row, curr.col-1,
                               curr.row-1, curr.col};
            for (int i = 0; i < nextSteps.length; i += 2) {
                int nextRow = nextSteps[i];
                int nextCol = nextSteps[i+1];
                if (0 > nextRow || nextRow == R || 0 > nextCol || nextCol == C) continue;
                int nextElimination = curr.k - grid[nextRow][nextCol];
                StepState newState = new StepState(curr.steps + 1, nextRow, nextCol, nextElimination);
                if (nextElimination >= 0 && !seen.contains(newState)) { // if not hit wall and not seen b4
                    seen.add(newState);
                    queue.addLast(newState);
                }
            }
        }
        return -1;
    }
}
```
