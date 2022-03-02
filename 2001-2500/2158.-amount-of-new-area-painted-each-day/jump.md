# Jump

Using array to mark the index that we have painted. Instead of simply marking 0s and 1s to represent the non-painted vs painted. We use the endIdx to mark. This will let us know two information, first is whether or not this has been painted, second is if this is painted where we should go next.

```java
class Solution {
    public int[] amountPainted(int[][] paint) {
        int[] line = new int[50001];
        int[] res = new int[paint.length];
        for (int i = 0; i < paint.length; i++) {
            int paintedCount = 0;
            int startIdx = paint[i][0], endIdx = paint[i][1];
            while (startIdx < endIdx) {
                int jump = Math.max(startIdx+1, line[startIdx]); // jump one or jump more
                if (line[startIdx] == 0) paintedCount++; // counting
                line[startIdx] = Math.max(endIdx, jump); // mark painted and jump
                startIdx = jump;
            }
            res[i] = paintedCount;
        }
        return res;
    }
}
```
