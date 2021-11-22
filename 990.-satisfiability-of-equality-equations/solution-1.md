# Solution 1

### Approach

Simple Union Find. Process equal equation first, If the equation is equal, group them together. If not then check if they are in the same group

```java
class Solution {
    int[] table;
    public boolean equationsPossible(String[] equations) {
        table = new int[26];
        for(int i = 0; i < 26; i++) table[i] = i;
        
        for(String equation : equations) {
            if (equation.charAt(1) == '!') continue;
            int p = equation.charAt(0) - 'a';
            int q = equation.charAt(3) - 'a';
            if (equation.charAt(1) == '=') {
                union(p, q);
            }
        }
        for(String equation : equations) {
            if (equation.charAt(1) == '=') continue;
            int p = equation.charAt(0) - 'a';
            int q = equation.charAt(3) - 'a';
            if (equation.charAt(1) == '!') {
                if (sameGroup(p, q)) return false;
            }
        }
        return true;
    }
    public void union(int p, int q) {
        int rootP = findRoot(p);
        int rootQ = findRoot(q);
        if (rootP != rootQ) {
            table[rootP] = rootQ;
        }
    }
    public int findRoot(int p) {
        if (p != table[p]) table[p] = findRoot(table[p]);
        return table[p];
    }
    public boolean sameGroup(int p, int q) {
        int rootP = findRoot(p);
        int rootQ = findRoot(q);
        return rootP == rootQ;
    }
}
```

### Take Away

`if (p != table[p]) table[p] = findRoot(table[p]);` This makes the findRoot operation become amortized O(1);

### Analysis

Amortize O(1) for findRoot, two for loops cost 2n. Overall time complexity is O(n).

Space complexity is O(26) for storing 26 characters.
