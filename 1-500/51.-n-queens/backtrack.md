# BackTrack

```java
class Solution {
    int N;
    public List<List<String>> solveNQueens(int n) {
        N = n;
        Stack<int[]> queensLocation = new Stack<>();
        List<List<String>> ret = new ArrayList<>();
        
        // edge case
        if (n == 2 || n == 3) return ret;
        if (n == 1) {
            ret.add(new ArrayList(Arrays.asList('Q')));
            return ret;
        }
        
        List<String> board = new ArrayList<>();
        boolean next = false; // to indicate move to next row
        int row = 0;
        int col = 0;
        int[] temp;
        while (row < N) {
            // find queen location for a row
            while (col < N) {
                if (isValid(row, col, board)) {
                    queensLocation.push(new int[]{row, col});
                    board.add(buildRow(col));
                    next = true;
                    break;
                } else {
                    col++;
                }
            }
            // move to next row
            if (next) {
                row++;
                col = 0;
                if (row == N) { // end
                    ret.add(new ArrayList(board));
                    temp = queensLocation.pop();
                    board.remove(temp[0]);
                    row = temp[0];
                    col = temp[1]+1;
                }
            } else { // exhausted solution, pop row before
                temp = queensLocation.pop();
                if (temp[0] == 0 && temp[1] == N-1) break;
                board.remove(temp[0]);
                col = temp[1]+1;
                row = temp[0];
            }
            next = false;
        }
        return ret;
    }
    public String buildRow(int n) {
        StringBuilder temp = new StringBuilder();
        for(int i = 0; i < N; i++) {
            if (i == n) temp.append('Q');
            else temp.append('.');
        }
        return temp.toString();
    }
    
    public boolean isValid(int row, int col, List<String> board) {
        for(int r = 0, i = 1; r < row; r++, i++) {
            if (board.get(r).charAt(col) == 'Q') return false;
            if (col - i > -1 && board.get(row-i).charAt(col-i) == 'Q') return false;
            if (col + i < N && board.get(row-i).charAt(col+i) == 'Q') return false;
        }
        return true;
    }
}
```
