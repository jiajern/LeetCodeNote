# Prefix Sum

### Approach

The approach is sort of like 2 sum. And using **prefix sum** allows us to compute the sum of any subarray quickly.

From left to right, compute the prefix sum. If the sum is equal to k then that's the longest so far.

If the sum is not equal to k, then we check if there exist the complement in the previous subarray. If there is then we compare if this new subarray's length is longer than the result we have so far, and takes the longest.

Next, we need to add the prefix sum to the map, if there is no existing entry. Because we want to have the longest subarray therefore we don't want to overwrite the existing prefix sum.

### Analysis

I learn the usage of the prefix sum.

Space used: O(n) for the map

Time used: O(n) by looping through the input array once.

### Code

```java
class Solution {
    public int maxSubArrayLen(int[] nums, int k) {
        int prefixSum = 0;
        int res = 0;
        Map<Integer, Integer> table = new HashMap<>();
        for(int i = 0; i < nums.length; i++) {
            prefixSum += nums[i];
            int complement = prefixSum - k;
            if (prefixSum == k) {
                res = i + 1;
            }
            if (table.containsKey(complement)) {
                res = Math.max(i - table.get(complement), res);
            }
            if (!table.containsKey(prefixSum)) {
                table.put(prefixSum, i);
            }
        }
        return res;
    }
}
```
