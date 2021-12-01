# Dynamic Programming

### Approach

Remember the best result of either rob or not rob

```java
class Solution {
    public int rob(int[] nums) {
        int rob = nums[0], noRob = 0;
        for(int i = 1; i < nums.length; i++) {
            int temp = noRob;
            noRob = rob; // if not robbing the current, then noRob will just equal to the best that we got from last rob
            rob = Math.max(rob, temp + nums[i]); // rob if it yield better result
        }
        return Math.max(rob, noRob);
    }
}
```
