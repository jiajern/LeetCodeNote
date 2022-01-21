# Iterative

### Code

```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        if (root == null) return result;
        Deque<TreeNode> deq = new ArrayDeque<>();
        TreeNode cur = root;
        do {
            while (cur != null) {
                deq.addLast(cur);
                cur = cur.left;
            }
            cur = deq.removeLast();
            result.add(cur.val);
            cur = cur.right;
        } while(cur != null || !deq.isEmpty());
        return result;
        
    }
}
```
