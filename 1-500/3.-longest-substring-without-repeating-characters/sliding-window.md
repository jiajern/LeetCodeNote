# Sliding Window

### Approach

Using **sliding window**. To quickly check if we have seen the character, make use of **set**. Keep adding the character into our hashset "window". When the character already exist in the window, we keep removing until the repeating character is removed.

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        Set<Character> seen = new HashSet<>();
        int ans = 0, i = 0, j = 0;
        while(j < s.length()) {
            if(!seen.contains(s.charAt(j))) {
                seen.add(s.charAt(j));
                ans = Math.max(ans, seen.size());
                j++;
            } else {
                seen.remove(s.charAt(i++));
            }
        }
        return ans;
    }
}
```
