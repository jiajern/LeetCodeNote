# Two Pointer

### Approach

When one end is greater than another end, the water trapped will depend on the lower end.

### Code

```java
class Solution {
    public int trap(int[] height) {
        int res = 0, left = 0, right = height.length - 1, leftmax = 0, rightmax = 0;
        while (left < right) {
            if (height[left] < height[right]) {
                if (height[left] > leftmax) leftmax = height[left];
                else res += leftmax - height[left];
                left++;
            } else {
                if (height[right] > rightmax) rightmax = height[right];
                else res += rightmax - height[right];
                right--;
            }
        }
        return res;
        
    }
}
```
