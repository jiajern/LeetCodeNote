# Recursion

### Code

```java
class Solution {
    Map<String, List<Integer>> table = new HashMap<>();
    
    public List<Integer> diffWaysToCompute(String expression) {
        List<Integer> result = new ArrayList<>();
        for (int i = 0; i < expression.length(); i++) {
            char currentChar = expression.charAt(i);
            if (currentChar == '+' || currentChar == '-' || currentChar == '*') {
                String leftExpression = expression.substring(0, i);
                String rightExpression = expression.substring(i+1, expression.length());
                List<Integer> left = table.getOrDefault(leftExpression, diffWaysToCompute(leftExpression));
                List<Integer> right = table.getOrDefault(rightExpression, diffWaysToCompute(rightExpression));
                for (Integer l : left) {
                    for (Integer r : right) result.add(evaluate(l, r, currentChar));
                }
            }
        }
        if (result.size() == 0) result.add(Integer.valueOf(expression));
        table.put(expression, result);
        return result;
    }
    
    public int evaluate(int l, int r, char c) {
        if (c == '+') return l + r;
        else if (c == '-') return l - r;
        else return l * r;
    }
}
```
