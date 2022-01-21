# Iterative

### Code

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        if (root == null) return result;
        Deque<TreeNode> deq = new ArrayDeque<>();
        TreeNode cur = root;
        while (cur != null) {
            if (cur.left != null) deq.addLast(cur.left);
            result.add(cur.val);
            if (cur.right == null && deq.isEmpty()) cur = null;
            else if (cur.right == null) cur = deq.removeLast();
            else cur = cur.right;
        }
        Collections.reverse(result);
        return result;
    }
}
```
