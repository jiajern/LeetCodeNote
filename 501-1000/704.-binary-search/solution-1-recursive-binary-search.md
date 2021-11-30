# Solution 1 Recursive Binary Search

### Approach

**Binary Search** with recursion

```java
class Solution {
    public int search(int[] nums, int target) {
        return binarySearch(nums, target, 0, nums.length - 1);
    }
    public int binarySearch(int[] nums, int target, int left, int right) {
        if (left > right) return -1;
        if (left == right) return nums[left] == target ? left : -1;
        int midIndex = (int)(right + left) / 2;
        if (nums[midIndex] == target) return midIndex;
        else if (nums[midIndex] > target) return binarySearch(nums, target, left, midIndex - 1);
        else return binarySearch(nums, target, midIndex + 1, right);
    }
}
```
