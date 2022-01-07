# Iterative

### Approach

Taking one element at a time and keep on adding it into the previous result.

### Code

```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> result1 = new ArrayList<>();
        List<List<Integer>> result2 = new ArrayList<>();
        result1.add(new ArrayList<>());
        result2.add(new ArrayList<>());
        for (int i = 0; i < nums.length; i++) {
            if (i % 2 == 0) {
                for (List<Integer> entry : result1) {
                    List<Integer> temp = new ArrayList<>(entry);
                    temp.add(nums[i]);
                    result2.add(temp);
                }
                result1 = new ArrayList<>(result2);
            } else {
                for (List<Integer> entry : result2) {
                    List<Integer> temp2 = new ArrayList<>(entry);
                    temp2.add(nums[i]);
                    result1.add(temp2);
                }
                result2 = new ArrayList<>(result1);
            }
        }
        
        return nums.length % 2 == 0 ? result1 : result2;
    }
}

```
