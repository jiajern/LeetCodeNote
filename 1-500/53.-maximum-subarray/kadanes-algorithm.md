# Kadane's Algorithm

### Code

```java
class Solution {
    public int maxSubArray(int[] nums) {
        int subarraySum = nums[0];
        int maxSubarraySum = nums[0];
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] > subarraySum + nums[i]) subarraySum = nums[i];
            else subarraySum += nums[i];
            maxSubarraySum = Math.max(subarraySum, maxSubarraySum);
        }
        return maxSubarraySum;
    }
}
```
