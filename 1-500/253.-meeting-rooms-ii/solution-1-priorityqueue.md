# Solution 1 PriorityQueue

Using **PriorityQueue**, to store the rooms that are being used. Before schedule a new meeting, we poll the one that end earlier than the start time of the new meeting.

```java
class Solution {
    public int minMeetingRooms(int[][] intervals) {
        Arrays.sort(intervals, (a, b) -> (a[0] - b[0]));
        Queue<int[]> rooms = new PriorityQueue<>(intervals.length, (a, b) -> (a[1] - b[1]));
        int roomNow = 0, result = 0;
        for(int[] interval : intervals) {
            if (rooms.peek() == null) {
                roomNow++;
                rooms.offer(interval);
            } else {
                while (rooms.peek() != null && rooms.peek()[1] <= interval[0]) {
                    rooms.poll();
                    roomNow--;
                }
                rooms.offer(interval);
                roomNow++;
            }
            result = Math.max(result, roomNow);
        }
        return result;
    }
}
```
