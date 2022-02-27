# DP Prefix Sum

Make use of something similar to prefix sum.

By tracking the maximum from left and maximum from right. We are able to get the maximum number at each element.

```java
class Solution {
    public long maxPoints(int[][] points) {
        int R = points.length;
        int C = points[0].length;
        if (R == 1 && C == 1) return points[0][0];
        long[] bestResultFromEachCol = new long[C];
        long bestResult = 0;
        // initialize
        for (int i = 0; i < C; i++) {
            if (points[0][i] > bestResult) bestResult = points[0][i];
            bestResultFromEachCol[i] = points[0][i];
        }
        for (int i = 1; i < R; i++) {
            long[] maxFromLeft = new long[C];
            long[] maxFromRight = new long[C];
            // build max from left
            for (int j = 0; j < C; j++) {
                if (j == 0) maxFromLeft[0] = bestResultFromEachCol[0];
                else {
                    maxFromLeft[j] = Math.max(bestResultFromEachCol[j], maxFromLeft[j-1]-1);
                }
            }
            // build max from right
            for (int j = C-1; j > -1; j--) {
                if (j == C-1) maxFromRight[C-1] = bestResultFromEachCol[C-1];
                else {
                    maxFromRight[j] = Math.max(bestResultFromEachCol[j], maxFromRight[j+1]-1);
                }
            }
            // compute each result and get best result
            for (int j = 0; j < C; j++) {
                bestResultFromEachCol[j] = points[i][j] + Math.max(maxFromLeft[j], maxFromRight[j]);
                if (bestResultFromEachCol[j] > bestResult) bestResult = bestResultFromEachCol[j];
            }
        }
        return bestResult;
            
    }
}
```
