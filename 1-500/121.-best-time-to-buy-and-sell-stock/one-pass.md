# One pass

### Approach

Loop through the array and look for the lowest. Take the current price and minus the lowest that we have seen so far will give us the best profit.

### Code

```java
class Solution {
    public int maxProfit(int[] prices) {
        int profit = 0, lowest = prices[0];
        for (int i = 1; i < prices.length; i++) {
            if (prices[i] < lowest) lowest = prices[i];
            else if (prices[i] - lowest > profit) profit = prices[i] - lowest;
        }
        return profit;
    }
}
```
