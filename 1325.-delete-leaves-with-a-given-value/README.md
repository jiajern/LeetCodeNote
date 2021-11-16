# 1325. Delete Leaves With a Given Value

{% embed url="https://leetcode.com/problems/delete-leaves-with-a-given-value" %}

### Description

Given a binary tree `root` and an integer `target`, delete all the **leaf nodes** with value `target`.

Note that once you delete a leaf node with value `target`**, **if it's parent node becomes a leaf node and has the value `target`, it should also be deleted (you need to continue doing that until you can't).

### Example

#### Example 1

![](https://assets.leetcode.com/uploads/2020/01/09/sample\_1\_1684.png)

```
Input: root = [1,2,3,2,null,2,4], target = 2
Output: [1,null,3,null,4]
Explanation: Leaf nodes in green with value (target = 2) are removed (Picture in left). 
After removing, new nodes become leaf nodes with value (target = 2) (Picture in center).
```

### Constraints

* `1 <= target <= 1000`
* The given binary tree will have between `1` and `3000` nodes.
* Each node's value is between `[1, 1000]`.
