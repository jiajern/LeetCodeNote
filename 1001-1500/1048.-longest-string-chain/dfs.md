# DFS

### Approach

Using DFS. Return the height of the node. 想象 root 是



```java
class Solution {
    public int longestStrChain(String[] words) {
        Set<String> seen = new HashSet<>();
        Map<String, Integer> height = new HashMap<>();
        // Arrays.sort(words, (a, b) -> b.length() - a.length());
        for (int i = 0; i < words.length; i++) seen.add(words[i]);
        int ret = 0;
        for (String w : words) {
            ret = Math.max(ret, dfs(seen, height, w));
        }
        
        return ret;
    }
    
    public int dfs(Set<String> seen, Map<String, Integer> height, String word) {
        if (height.containsKey(word)) return height.get(word);
        int h = 1;
        StringBuilder sb = new StringBuilder(word);
        for (int i = 0; i < word.length(); i++) {
            String potentialChild = sb.deleteCharAt(i).toString();
            if (seen.contains(potentialChild)) {
                int currentHeight = 1 + dfs(seen, height, potentialChild);
                h = Math.max(h, currentHeight);
            }
            sb.insert(i, word.charAt(i));
        }
        height.put(word, h);
        return h;
    }
}
```
