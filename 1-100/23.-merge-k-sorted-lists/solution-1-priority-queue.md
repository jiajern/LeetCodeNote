# Solution 1 Priority Queue

### Approach

Using **PriorityQueue **as **min heap**. We put all the elements into the heap. Then pop it out again

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
    public ListNode mergeKLists(ListNode[] lists) {
        ListNode res = new ListNode(-1);
        ListNode cursor = res;
        PriorityQueue<ListNode> minHeap = new PriorityQueue<ListNode>((ListNode a, ListNode b) -> a.val - b.val);
        for(int i = 0; i < lists.length; i++) {
            if(lists[i] != null) {
                minHeap.add(lists[i]);
            }
        }
        while(minHeap.size() > 0) {
            ListNode temp = minHeap.poll();
            cursor.next = temp;
            cursor = cursor.next;
            if(temp.next != null) {
                minHeap.add(temp.next);
            }
        }
        return res.next;
    }
}
```

### Analysis

The heap will take operation O(log n) for insert element and removing element. So the overall time complexity will be O(n log n)

Space will be O(n) for n element

### Take away

* priority queue
