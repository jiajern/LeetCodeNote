# Binary Search

### Approach

**Binary Search** keep moving the left, make sure right is always greater than target.

```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        int left = 0, n = nums.length, right = n - 1;
        while(left < right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) return mid;
            else if (nums[mid] > target) right = mid;
            else left = mid + 1;
        }
        if (nums[left] < target && left == n - 1) return left + 1;
        else return left;
    }
}
```
