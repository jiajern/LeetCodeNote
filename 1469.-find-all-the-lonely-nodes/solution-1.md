# Solution 1

Recursively traversing the tree then append it into the list. Top down solution

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
    public List<Integer> getLonelyNodes(TreeNode root) {
        List<Integer> nodes = new ArrayList<>();
        getLonelyNodes(root, false, nodes);
        return nodes;
    }
    private void getLonelyNodes(TreeNode root, boolean isLonely, List<Integer> nodes) {
        if (root == null) return;

        if (isLonely) {
            nodes.add(root.val);
        }
        getLonelyNodes(root.left, root.right == null, nodes);
        getLonelyNodes(root.right, root.left == null, nodes);
    }
}
```
