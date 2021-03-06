# 1522. Diameter of N-Ary Tree

{% embed url="https://leetcode.com/problems/diameter-of-n-ary-tree" %}

### Description

Given a `root` of an [N-ary tree](https://leetcode.com/articles/introduction-to-n-ary-trees/), you need to compute the length of the diameter of the tree.

The diameter of an N-ary tree is the length of the **longest** path between any two nodes in the tree. This path may or may not pass through the root.

(_Nary-Tree input serialization is represented in their level order traversal, each group of children is separated by the null value.)_

### _Example_

#### _Example 1_

![](https://assets.leetcode.com/uploads/2020/07/19/sample\_2\_1897.png)

```
Input: root = [1,null,3,2,4,null,5,6]
Output: 3
Explanation: Diameter is shown in red color.
```

#### Example 2

![](https://assets.leetcode.com/uploads/2020/07/19/sample\_1\_1897.png)

```
Input: root = [1,null,2,null,3,4,null,5,null,6]
Output: 4
```

### Constraints

* The depth of the n-ary tree is less than or equal to `1000`.
* The total number of nodes is between `[1, 10^4]`.
