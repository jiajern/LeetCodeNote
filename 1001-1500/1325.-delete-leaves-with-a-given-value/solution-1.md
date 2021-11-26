# Solution 1

### Approach

Recursively traversing through the tree. Apply the same algorithm to all subtree. If node is the target simply return true.

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
    public TreeNode removeLeafNodes(TreeNode root, int target) {
        return myTrim(root, target);
    }
    public TreeNode myTrim(TreeNode node, int target) {
        if (node.left != null) node.left = myTrim(node.left, target);
        if (node.right != null) node.right = myTrim(node.right, target);
        return node.val == target && node.left == null && node.right == null ? null : node;
    }
}
```
