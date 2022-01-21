# Iterative

### Code

```java
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        if (root == null) return result;
        Deque<TreeNode> deq = new ArrayDeque<>();
        TreeNode cur = root;
        do {
            if (cur.right != null) deq.addLast(cur.right);
            result.add(cur.val);
            if (cur.left == null && deq.isEmpty()) cur = null;
            else if (cur.left == null) cur = deq.removeLast();
            else cur = cur.left;
        } while (cur != null);
        return result;
    }
}
```
