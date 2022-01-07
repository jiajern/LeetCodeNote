# Post Order Traversal

### Approach

Using **post order traversal** to find out all the subtree's sum. Then see which sum can make the best product.

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
    private static final int MOD = 1000000007;
    List<Integer> prefixSum;
    public int maxProduct(TreeNode root) {
        prefixSum = new ArrayList<>();
        long finalSum = postorder(root);
        // int half = (int) finalSum / 2;
        // int closestToHalf = Integer.MAX_VALUE;
        // for (Integer i : prefixSum) {
        //     if (Math.abs(i - half) < Math.abs(closestToHalf - half)) closestToHalf = i;
        // }
        // return (closestToHalf * (finalSum - closestToHalf)) % MOD;
        long bestProductSoFar = 0;
        for (long i : prefixSum) {
            bestProductSoFar = Math.max(i * (finalSum - i), bestProductSoFar);
        }
        return (int)(bestProductSoFar % MOD);
    }
    public int postorder(TreeNode node) {
        if (node == null) return 0;
        int leftSum = postorder(node.left);
        int rightSum = postorder(node.right);
        int total = leftSum + rightSum + node.val;
        prefixSum.add(total);
        return total;
    }
}
```
