# HashMap

### Approach

Record where the change will happen and insert the changes instead of the original string.

First iterate through the string and use **startsWith** to check for match. If there is a match, we want to record it so we will take this change.

Second iteration will be just going through the string and see if change should be applied. If so then apply then changes, else append the original string.

### Code

```java
class Solution {
    public String findReplaceString(String s, int[] indices, String[] sources, String[] targets) {
        // sources is what we try to find match
        // targets is what we want to change to
        // indices is where we should check for match and replace
        Map<Integer, Integer> table = new HashMap<>(); // indexInS, the i-th targets
        for (int i = 0; i < indices.length; i++) {
            if (s.startsWith(sources[i], indices[i])) { // if see match
                table.put(indices[i], i);
            }
        }
        
        StringBuilder sb = new StringBuilder();
        // iterate through s
        for (int i = 0; i < s.length(); i++) {
            if (table.containsKey(i)) {
                sb.append(targets[table.get(i)]);
                i += sources[table.get(i)].length() - 1;
            } else {
                sb.append(s.charAt(i));
            }
        }
        return sb.toString();
    }
}
```
