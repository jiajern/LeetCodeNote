# Solution 1

### Approach

Using the height, all the nodes that will be removed together has the same height

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
    private List<Pair<Integer, Integer>> pairs;
    
    private int getHeight(TreeNode node) {
        if (node == null) return -1;
        int leftHeight = getHeight(node.left);
        int rightHeight = getHeight(node.right);
        int currHeight = Math.max(leftHeight, rightHeight) + 1;
        this.pairs.add(new Pair<Integer, Integer>(currHeight, node.val));
        return currHeight;
    }
    public List<List<Integer>> findLeaves(TreeNode root) {
        this.pairs = new ArrayList<>();
        getHeight(root);
        Collections.sort(this.pairs, Comparator.comparing(p -> p.getKey()));
        int n = this.pairs.size(), height = 0, i = 0;
        List<List<Integer>> ret = new ArrayList<>();
        
        while(i < n) {
            List<Integer> nums = new ArrayList<>();
            while(i < n && this.pairs.get(i).getKey() == height) {
                nums.add(this.pairs.get(i).getValue());
                i++;
            }
            height++;
            ret.add(nums);
        }
        return ret;
    }
}
```
