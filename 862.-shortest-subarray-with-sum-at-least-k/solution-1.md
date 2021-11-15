# Solution 1

### Approach

Using **prefix sum** and **monoqueue** approach. The key is that **k** is positive. So we make P\[0] = 0 and whenever our subarray sum drop below the previous number we remove the previous. It doens't matter if it drop in the middle. The key of P\[0] is to prevent we get the subarray sum equal to negative. At this point we should give up "0" then start with new.

```java
class Solution {
    public int shortestSubarray(int[] nums, int k) {
        int N = nums.length;
        long[] P = new long[N+1];
        for(int i = 0; i < N; i++) {
            P[i + 1] = P[i] + (long) nums[i];
        }
        int ans = N+1;
        Deque<Integer> monoq = new LinkedList<>();
        
        for(int y = 0; y < P.length; ++y) {
            while(!monoq.isEmpty() && P[y] <= P[monoq.getLast()]) {
                monoq.removeLast();
            }
            while(!monoq.isEmpty() && P[y] >= P[monoq.getFirst()] + k) {
                ans = Math.min(ans, y - monoq.removeFirst());
            }
            monoq.addLast(y);
        }
        return ans < N+1 ? ans : -1;
    }
}
```

{% embed url="https://docs.google.com/presentation/d/1b47XvvtrUzPPE3Uy-2N9jzDUk2UscehjmQy8hlctHZA/edit?usp=sharing" %}
