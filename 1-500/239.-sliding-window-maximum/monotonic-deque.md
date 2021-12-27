# Monotonic Deque

### Approach

Using **monotonic decreasing deque** to maintain the largest seen so far.

```java

class Solution {
    Deque<Integer> deque = new ArrayDeque<>();
    
    public void cleanDeque(int[] nums, int i, int k) {
        if (!deque.isEmpty() && deque.getFirst() == i - k) deque.removeFirst();
        while(!deque.isEmpty() && nums[deque.getLast()] < nums[i]) deque.removeLast();
    }
    public int[] maxSlidingWindow(int[] nums, int k) {
        int N = nums.length;
        int[] ret = new int[N-k+1];
        for (int i = 0; i < N; i++) {
            cleanDeque(nums, i, k);
            deque.addLast(i);
            if (i >= k-1) ret[i-k+1] = nums[deque.getFirst()];
        }
        ret[N-k] = nums[deque.getFirst()];
        return ret;
    }
}
```
