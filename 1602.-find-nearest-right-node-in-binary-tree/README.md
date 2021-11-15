# 1602. Find Nearest Right Node in Binary Tree

{% embed url="https://leetcode.com/problems/find-nearest-right-node-in-binary-tree" %}
link to the question
{% endembed %}

### **Description**

Given the `root` of a binary tree and a node `u` in the tree, return _the **nearest** node on the **same level** that is to the **right** of_ `u`_, or return_ `null` _if _`u` _is the rightmost node in its level_.

### **Example**

#### **Example 1**

![](https://assets.leetcode.com/uploads/2020/09/24/p3.png)

```
Input: root = [1,2,3,null,4,5,6], u = 4
Output: 5
Explanation: The nearest node on the same level to the right of node 4 is node 5.
```

#### Example 2

![](https://assets.leetcode.com/uploads/2020/09/23/p2.png)

```
Input: root = [3,null,4,2], u = 2
Output: null
Explanation: There are no nodes to the right of 2.
```

### Constraints

* The number of nodes in the tree is in the range `[1, 105]`.
* `1 <= Node.val <= 105`
* All values in the tree are **distinct**.
* `u` is a node in the binary tree rooted at `root`.
