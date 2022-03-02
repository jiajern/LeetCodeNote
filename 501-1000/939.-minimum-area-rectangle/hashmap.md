# HashMap

Record all the points that we have seen so far. So we can quickly check if we have the required points to construct the whole rectangle.

```java
class Solution {
    public int minAreaRect(int[][] points) {
        Map<Integer, Set<Integer>> seen = new HashMap<>();
        for (int[] p : points) {
            if (!seen.containsKey(p[0])) seen.put(p[0], new HashSet<>());
            seen.get(p[0]).add(p[1]);
        }
        int result = Integer.MAX_VALUE;
        for (int[] p1 : points) {
            for (int[] p2 : points) {
                if (p1[0] == p2[0] || p1[1] == p2[1]) continue;
                if (seen.get(p1[0]).contains(p2[1]) && seen.get(p2[0]).contains(p1[1])) {
                    result = Math.min(result, Math.abs(p1[0] - p2[0]) * Math.abs(p1[1] - p2[1]));
                }
            }
        }
        return result == Integer.MAX_VALUE ? 0 : result;
    }
}
```
