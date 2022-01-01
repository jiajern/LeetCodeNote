# DFS

### Approach

Using **DFS** recursively to solve the problem. When using DFS it will keep going down eventually return.

### Code

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    int K;
    List<Integer> ans;
    TreeNode target;
    
    public List<Integer> distanceK(TreeNode root, TreeNode target, int k) {
        ans = new LinkedList<>();
        this.target = target;
        this.K = k;
        dfs(root);
        return ans;
    }
    
    public int dfs(TreeNode node) {
        if (node == null) return -1;
        if (node == target) {
            addSubtree(node, 0);
            return 1;
        }
        int L = dfs(node.left);
        int R = dfs(node.right);
        if (L != -1) {
            if (L == K) ans.add(node.val);
            addSubtree(node.right, L + 1);
            return L + 1;
        } else if (R != -1) {
            if (R == K) ans.add(node.val);
            addSubtree(node.left, R + 1);
            return R + 1;
        } else return -1;
    }
    
    public void addSubtree(TreeNode node, int dist) {
        if (node == null) return;
        if (dist == K) ans.add(node.val);
        else {
            addSubtree(node.left, dist+1);
            addSubtree(node.right, dist+1);
        }
    }
}
```
