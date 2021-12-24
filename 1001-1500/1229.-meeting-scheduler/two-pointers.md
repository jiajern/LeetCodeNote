# Two Pointers

### Approach

To find the intersection interval:

* start = Math.max(slots1\[pointer1]\[0], slots2\[pointer2]\[0]);
* end = Math.min(slots1\[pointer1]\[1], slots2\[pointer2]\[1]);

If this is within the duration, then we have our result. **If not then move the pointer that end earlier.**

### Code

```java
class Solution {
    public List<Integer> minAvailableDuration(int[][] slots1, int[][] slots2, int duration) {
        Arrays.sort(slots1, (a, b) -> a[0] - b[0]);
        Arrays.sort(slots2, (a, b) -> a[0] - b[0]);
        
        int pointer1 = 0, pointer2 = 0;
        
        while (pointer1 < slots1.length && pointer2 < slots2.length) {
            int intersectLeft = Math.max(slots1[pointer1][0], slots2[pointer2][0]);
            int intersectRight = Math.min(slots1[pointer1][1], slots2[pointer2][1]);
            if (intersectRight - intersectLeft >= duration) return new ArrayList<Integer>(Arrays.asList(intersectLeft, intersectLeft + duration));
            if (slots1[pointer1][1] < slots2[pointer2][1]) pointer1++;
            else pointer2++;
        }
        return new ArrayList<Integer>();
    }
}
```
