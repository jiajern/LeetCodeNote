# Two Pointers

### Code

```java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int p1 = m - 1, p2 = n - 1, p3 = n + m - 1;
        while(p1 > -1 || p2 > -1) {
            if(p1 != -1 && p2 != -1 && nums1[p1] > nums2[p2]) {
                nums1[p3] = nums1[p1];
                p3--;
                p1--;
            }else if(p1 != -1 && p2 != -1 && nums1[p1] <= nums2[p2]) {
                nums1[p3] = nums2[p2];
                p3--;
                p2--;
            }else if(p1 != -1 && p2 == -1) {
                nums1[p3] = nums1[p1];
                p3--;
                p1--;
            }else if(p1 == -1 && p2 != -1) {
                nums1[p3] = nums2[p2];
                p3--;
                p2--;
            }
        }
    }
}

```
