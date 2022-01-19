# Two Pointer

### Code

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        if(head == null || head.next == null) { return false; }
        ListNode faster = head;
        ListNode slower = head;
        while(faster != null) {
            faster = faster.next != null ? faster.next.next : null;
            slower = slower.next;
            if(faster == slower && faster != null) {
                return true;
            }
        }
        return false;
    }
}
```
