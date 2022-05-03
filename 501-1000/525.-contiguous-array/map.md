# Map

### Approach

Add one if encounter ones, minus one if encounter zero.

If we encounter the same **count** again, it implies the subarray is found. Why is that? think of it as a graph, it will form a V or upsidedown.

If we encounter zero, that also means the subarray is found.

we can initialize the map with 0, -1

### Learn

This is sort of like dynamic programming i guess.

Time complexity: O(n) for looping through the input array

Space complexity: O(n) for storing the count at each index.

### Code

```java
class Solution {
    public int findMaxLength(int[] nums) {
        Map<Integer, Integer> table = new HashMap<>();
        int res = 0, count = 0;
        table.put(count, -1);
        for (int i = 0; i < nums.length; i++) {
            count = nums[i] == 0 ? count - 1 : count + 1;
            if (table.containsKey(count)) {
                res = Math.max(res, i - table.get(count));
            } else {
                table.put(count, i);
            }
        }
        return res;
    }
}
```
