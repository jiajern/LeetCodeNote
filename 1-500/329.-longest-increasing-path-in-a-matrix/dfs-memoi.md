# DFS Memoi

```java
class Solution {
    Map<Integer, Integer> memo;
    int R;
    int C;
    
    public int longestIncreasingPath(int[][] matrix) {
        memo = new HashMap<>();
        R = matrix.length; 
        C = matrix[0].length;
        if (R == 1 && C == 1) return 1;
        // generate the longest path can be traveled from each node
        for (int i = 0; i < R*C; i++) {
            explore(matrix, i);
        }
        int longest = 0;
        // find which one is longest and return
        for (Integer key : memo.keySet()) {
            if (memo.get(key) > longest) longest = memo.get(key);
        }
        return longest;
    }
    // return the longest path can be traveled from given node
    public int explore(int[][] matrix, int coord) {
        if (memo.containsKey(coord)) return memo.get(coord);
        int row = coord / C;
        int col = coord % C;
        int[] nextNodes = {
            row-1, col,
            row, col+1,
            row+1, col,
            row, col-1
        };
        int longest = 0;
        for (int i = 0; i < nextNodes.length; i+=2) {
            int nextRow = nextNodes[i];
            int nextCol = nextNodes[i+1];
            if (nextRow < 0 || nextRow >= R || nextCol < 0 || nextCol >= C) continue;
            if (matrix[nextRow][nextCol] >= matrix[row][col]) continue;
            int nextCoord = nextRow * C + nextCol;
            int temp = explore(matrix, nextCoord);
            if (longest < temp) longest = temp;
        }
        memo.put(coord, longest+1);
        return longest + 1;
    }
}
```
