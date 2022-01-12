# Hash Table

### Approach

Using **hashmap** to store all the element we have seen. Check if the "complement" exist. If it does, then we find our target. If not then keep moving and add the current number into the "seen" hash table

### Code

```java
public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> seen = new HashMap<>();
        for(int i = 0; i < nums.length; i++) {
            int complement = target - nums[i];
            if(seen.containsKey(complement)) {
                return new int[]{seen.get(complement), i};
            } else {
                seen.put(nums[i], i);
            }
        }
        return null;
    }
```
