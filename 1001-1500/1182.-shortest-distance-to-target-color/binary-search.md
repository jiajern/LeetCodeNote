# Binary Search

### Approach

Use map to keep the list of index for the color. Then using **Binary Search** to find the closest.

### Code

```java
class Solution {
    public List<Integer> shortestDistanceColor(int[] colors, int[][] queries) {
        List<Integer> ret = new ArrayList<>();
        Map<Integer, List<Integer>> map = new HashMap<>();
        map.put(1, new ArrayList<>());
        map.put(2, new ArrayList<>());
        map.put(3, new ArrayList<>());
        for(int i = 0; i < colors.length; i++) {
            map.get(colors[i]).add(i);
        }
        for(int[] q : queries) {
            ret.add(bisearch(map.get(q[1]), q[0]));
        }
        return ret;
    }
    
    public int bisearch(List<Integer> list, int target) {
        if (list.size() == 0) return -1;
        int left = 0, right = list.size() - 1, mid = 0;
        if (target > list.get(right)) return target - list.get(right);
        if (target < list.get(left)) return list.get(left) - target;
        while(left <= right) {
            mid = left + (right - left) / 2;
            if (list.get(mid) == target) return 0;
            else if (list.get(mid) > target) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }
        return (list.get(left) - target) < (target - list.get(right)) ? list.get(left) - target : target - list.get(right);
    }
}
```
