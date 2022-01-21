# Recursive

### Code

```java
class Solution {
    List<Integer> result;
    public List<Integer> preorderTraversal(TreeNode root) {
        result = new ArrayList<>();
        helper(root);
        return result;
    }
    public void helper(TreeNode node) {
        if (node == null) return;
        result.add(node.val);
        helper(node.left);
        helper(node.right);
    }
}
```
