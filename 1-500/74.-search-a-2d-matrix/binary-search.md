# Binary Search

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int R = matrix.length, C = matrix[0].length;
        int left = 0, right = (R * C) - 1;
        while(left <= right) {
            int mid = (right - left / 2) + left;
            int row = mid / C, col = mid % C;
            if (matrix[row][col] == target) return true;
            if (matrix[row][col] > target) right = mid - 1;
            else left = mid + 1;
        }
        return false;
    }
}
```
