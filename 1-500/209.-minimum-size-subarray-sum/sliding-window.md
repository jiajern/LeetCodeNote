# Sliding Window

### Approach

Think of a window that we want to minimize its size. First, we expand the window until we meet the condition which is `total >= target` then we try to decrease the window size by taking out the leftmost element.

### Analysis

This is like sliding window, two pointers, prefix sum.

Time complexity: O(n) looping through the input array O(n) to remove the leftmost element.

Space: O(1) no extra space allocated

### Code

```java
class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        int ans = Integer.MAX_VALUE;
        int left = 0, total = 0;
        for (int i = 0; i < nums.length; i++) {
            total += nums[i];
            while (total >= target) {
                ans = Math.min(ans, i + 1 - left);
                total = total - nums[left++]; // getting rid of leftmost element
            }
        }
        return ans == Integer.MAX_VALUE ? 0 : ans;
    }
}
```
