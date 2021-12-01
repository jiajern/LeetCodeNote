# Cyclic Switching

### Approach

Keep switching the element until all element are swapped

```java
class Solution {
    public void rotate(int[] nums, int k) {
        k = k % nums.length;
        int count = 0;
        for(int start = 0; count < nums.length; start++) {
            int currentIdx = start;
            int prevNumber = nums[start];
            do {
                int nextIdx = (currentIdx + k) % nums.length;
                prevNumber = place(nums, prevNumber, nextIdx);
                currentIdx = nextIdx;
                count++;
            } while (start != currentIdx);
        }
    }
    public int place(int[] nums, int prev, int i) {
        int temp = nums[i];
        nums[i] = prev;
        return temp;
    }
}
```
