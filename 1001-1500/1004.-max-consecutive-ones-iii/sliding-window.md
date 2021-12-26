# Sliding Window

### Approach

Think about maximizing the window only.

```java
class Solution {
    public int longestOnes(int[] nums, int k) {
        int left = 0, right = 0;
        while (right < nums.length) {
            if (nums[right++] == 0) k--;
            if (k < 0) {
                k += 1 - nums[left++];
            }
        }
        return right - left;
    }
}
```
