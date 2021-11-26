# Solution 1

### Approach

This is similar to&#x20;

{% content-ref url="../../1501-2000/1522.-diameter-of-n-ary-tree/" %}
[1522.-diameter-of-n-ary-tree](../../1501-2000/1522.-diameter-of-n-ary-tree/)
{% endcontent-ref %}

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
    int maxSum = Integer.MIN_VALUE;
    public int maxGain(TreeNode node) {
        if (node == null) return 0;
        
        int leftMax = Math.max(maxGain(node.left), 0);
        int rightMax = Math.max(maxGain(node.right), 0);
        int currentMax = leftMax + rightMax + node.val;
        
        this.maxSum = Math.max(this.maxSum, currentMax);
        return node.val + Math.max(leftMax, rightMax);
    }
    public int maxPathSum(TreeNode root) {
        maxGain(root);
        return this.maxSum;
    }
}
```
