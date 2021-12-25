# Sliding Window

```java
class Solution {
    public int lengthOfLongestSubstringTwoDistinct(String s) {
        Map<Character, Integer> seen = new HashMap<>();
        int left = 0, right = 0, res = 0;
        while (right < s.length()) {
            seen.put(s.charAt(right), right++);
            if (seen.size() > 2) {
                int del_idx = Collections.min(seen.values());
                int removedIdx = seen.remove(s.charAt(del_idx));
                left = removedIdx + 1;
            }
            res = Math.max(res, right - left);
        }
        return res;
    }
}
```
