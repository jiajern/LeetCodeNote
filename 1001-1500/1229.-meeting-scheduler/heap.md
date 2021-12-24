# Heap

### Approach

Using **Heap** so all slot are sorted by the start time. Since there will be no conflict for a person we can store the slot for both person in one heap.

Check if the end time of previous slot is overlap with the start of next

### Code

```java
class Solution {
    public List<Integer> minAvailableDuration(int[][] slots1, int[][] slots2, int duration) {
        PriorityQueue<int[]> heap = new PriorityQueue<>((a, b) -> a[0] - b[0]);
        
        for(int[] s : slots1) {
            if (s[1] - s[0] >= duration) heap.offer(s);
        }
        for(int[] s : slots2) {
            if (s[1] - s[0] >= duration) heap.offer(s);
        }
        
        while (heap.size() > 1) {
            int[] slot1 = heap.poll();
            int[] slot2 = heap.peek();
            if (slot1[1] >= slot2[0] + duration) return new ArrayList<>(Arrays.asList(slot2[0], slot2[0] + duration));
        }
        return new ArrayList<Integer>();
    }
}
```
