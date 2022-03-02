# Custom Object



```java
class TrieNode {
    private TrieNode[] links;
    private final int R = 26;
    private boolean isEnd;
    
    public TrieNode() {
        links = new TrieNode[R];
    }
    public boolean containsKey(char ch) {
        return links[ch-'a'] != null;
    }
    public TrieNode get(char ch) {
        return links[ch-'a'];
    }
    public void put(char ch, TrieNode node) {
        links[ch-'a'] = node;
    }
    public void setEnd() {
        isEnd = true;
    }
    public boolean isEnd() {
        return isEnd;
    }
}

class Trie {
    private TrieNode root;

    public Trie() {
        root = new TrieNode();
    }
    
    public void insert(String word) {
        TrieNode ptr = root;
        for (char c : word.toCharArray()) {
            if (!ptr.containsKey(c)) ptr.put(c, new TrieNode());
            ptr = ptr.get(c);
        }
        ptr.setEnd();
    }
    private TrieNode mySearch(String word) {
        TrieNode ptr = root;
        for (char c : word.toCharArray()) {
            if (!ptr.containsKey(c)) return null;
            ptr = ptr.get(c);
        }
        return ptr;
    }
    public boolean search(String word) {
        TrieNode node = mySearch(word);
        return node == null ? false : node.isEnd();
    }
    
    public boolean startsWith(String prefix) {
        TrieNode node = mySearch(prefix);
        return node == null ? false : true;
    }
}

/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.insert(word);
 * boolean param_2 = obj.search(word);
 * boolean param_3 = obj.startsWith(prefix);
 */
```
