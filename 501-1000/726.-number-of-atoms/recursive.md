# Recursive

When we meet the open parenthesis "(" we recursively compute the counter of each atom. The hardest part is to write a bug free solution. Careful with each testcase.

```java
class Solution {
    public String countOfAtoms(String formula) {
        StringBuilder result = new StringBuilder();
        Map<String, Integer> counter = parseFormula(formula, 0);
        for (String key : counter.keySet()) {
            if (key.equals("index")) continue;
            result.append(key);
            if (counter.get(key) > 1) result.append(counter.get(key));
        }
        return result.toString();
    }
    public Map<String, Integer> parseFormula(String formula, int startIdx) {
        Map<String, Integer> ret = new TreeMap<>();
        StringBuilder temp = new StringBuilder();
        int i = startIdx;
        int L = formula.length();
        for (; i < L && formula.charAt(i) != ')'; i++) {
            char currentChar = formula.charAt(i);
            if (currentChar == '(') {
                if (temp.length() > 0) {
                    ret.put(temp.toString(), ret.getOrDefault(temp.toString(), 0) + 1);
                    temp = new StringBuilder();
                }
                Map<String, Integer> nestedCount = parseFormula(formula, i+1);
                i = nestedCount.get("index");
                int multiplier = 1;
                if (i+1 < L && Character.isDigit(formula.charAt(i+1))) {
                    int val = Character.getNumericValue(formula.charAt(++i));
                    while (i+1 < L && Character.isDigit(formula.charAt(i+1))) {
                        val = val*10 + Character.getNumericValue(formula.charAt(++i));
                    }
                    multiplier = val;
                }
                for (String key : nestedCount.keySet()) {
                    if (key.equals("index")) continue;
                    ret.put(key, ret.getOrDefault(key, 0) + (nestedCount.get(key) * multiplier));
                }
            } else {
                if (Character.isDigit(currentChar)) {
                    int val = Character.getNumericValue(currentChar);
                    while (i+1 < L && Character.isDigit(formula.charAt(i+1))) {
                        val = val*10 + Character.getNumericValue(formula.charAt(++i));
                    }
                    ret.put(temp.toString(), ret.getOrDefault(temp.toString(), 0) + val);
                    temp = new StringBuilder();
                } else if (Character.isLowerCase(currentChar)) {
                    temp.append(currentChar);
                } else if (Character.isUpperCase(currentChar) && temp.length() != 0) {
                    ret.put(temp.toString(), ret.getOrDefault(temp.toString(), 0) + 1);
                    temp = new StringBuilder();
                    temp.append(currentChar);
                } else {
                    temp.append(currentChar);
                }
            }
        }
        if (temp.length() != 0) {
            ret.put(temp.toString(), ret.getOrDefault(temp.toString(), 0) + 1);
        }
        ret.put("index", i);
        return ret;
    }
}
```
