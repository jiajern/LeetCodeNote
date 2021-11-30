# Binary Search

### Approach

**Binary Search**

```java
/* The isBadVersion API is defined in the parent class VersionControl.
      boolean isBadVersion(int version); */

public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
        if (n == 1) return 1;
        int left = 1, right = n;
        boolean isRight = true;
        while(left < right) {
            int pivot = left + (right - left) / 2;
            if (isBadVersion(pivot)) right = pivot; // if is bad we want to keep it
            else left = pivot + 1; // if not bad then we can increment
        }
        return left;
    }
}
```

### **Take away**

Using **** `left + (right - left) / 2;` prevent left and right being too large and cause overflow
