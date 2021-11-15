# Solution 1

Using DFS and sentinel value to differentiate the level

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
    public TreeNode findNearestRightNode(TreeNode root, TreeNode u) {
        if (root == null) return null;
        
        Queue<TreeNode> queue = new LinkedList<>(){{
            offer(root);
            offer(null);
        }};
        TreeNode curr = null;
        
        while(!queue.isEmpty()) {
            curr = queue.poll();
            
            if (curr != null) {
                if (curr == u) {
                    return queue.poll();
                }
                if (curr.left != null) {
                    queue.offer(curr.left);
                }
                if (curr.right != null) {
                    queue.offer(curr.right);
                }
            } else {
                if (!queue.isEmpty()) {
                    queue.offer(null);
                }
            }
        }
        return null;
    }
}
```
