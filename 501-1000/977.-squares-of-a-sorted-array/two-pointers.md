# Two pointers

### Approach

using **Two Pointer** this is like merging two sorted array

```java
class Solution {
    public int[] sortedSquares(int[] nums) {
        int N = nums.length, left = 0, right = N - 1, i = N - 1;
        int[] ret = new int[N];
        int leftSquare = nums[left] * nums[left], rightSquare = nums[right] * nums[right];
        while(left < right) {
            if (leftSquare > rightSquare) {
                ret[i--] = leftSquare;
                left++;
                leftSquare = nums[left] * nums[left];
            } else {
                ret[i--] = rightSquare;
                right--;
                rightSquare = nums[right] * nums[right];
            }
        }
        ret[i] = leftSquare;
        return ret;
    }
}
```
