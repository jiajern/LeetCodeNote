# Loop

### Approach

Simply loop through and weave the linked list. Draw on paper will be easier to understand. Within the while condition, we only check for c2 because if we have odd/even number of element, c2 will always run out of element first or at the same time as c1.

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode oddEvenList(ListNode head) {
        if (head == null || head.next == null || head.next.next == null) return head;
        ListNode c1 = head, c2 = head.next, head2 = c2;
        while (c2 != null && c2.next != null) {
            c1.next = c1.next.next;
            c2.next = c2.next.next;
            c1 = c1.next;
            c2 = c2.next;
        }
        c1.next = head2;
        return head;
    }
}
```
