# Sliding Window

```java
class Solution {
    public int lengthOfLongestSubstringKDistinct(String s, int k) {
        int left = 0, right = 0, res = 0;
        Map<Character, Integer> seen = new HashMap<>();
        while (right < s.length()) {
            seen.put(s.charAt(right), right);
            if (seen.size() > k) {
                int removeIdx = Collections.min(seen.values());
                left = seen.remove(s.charAt(removeIdx)) + 1;
            }
            right++;
            res = Math.max(res, right - left);
        }
        return res;
    }
}
```
