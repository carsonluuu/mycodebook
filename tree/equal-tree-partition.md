# [Equal Tree Partition](https://leetcode.com/problems/equal-tree-partition/description/)

Given a binary tree with`n`nodes, your task is to check if it's possible to partition the tree to two trees which have the equal sum of values after removing **exactly **one edge on the original tree.

### Example

**Example 1:**

```
Input:     
    5
   / \
  10 10
    /  \
   2   3

Output: True
Explanation: 
    5
   / 
  10

Sum: 15

   10
  /  \
 2    3

Sum: 15
```

**Example 2:**

```
Input:
    1
   / \
  2  10
    /  \
   2   20
Output: False
Explanation: You can't split the tree into two trees 
             with equal sum after removing exactly one edge on the tree.
```

### **Note**

按edge划分子树

找sum/2的子树和就行！

### Code

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public boolean checkEqualTree(TreeNode root) {
        if (root == null) {
            return false;
        }
        int total = sum(root);
        boolean[] res = new boolean[1];
        sum(root.left,  total, res);
        sum(root.right, total, res);

        return res[0];
    }

    private int sum(TreeNode root) {
        if (root == null) {
            return 0;
        }

        return root.val + sum(root.left) + sum(root.right);
    }

    private int sum(TreeNode root, int total, boolean[] res) {
        if (root == null) {
            return 0;
        }

        int sum = root.val + sum(root.left, total, res) + sum(root.right, total, res);
        if (sum * 2 == total) {
            res[0] = true;
        }

        return sum;
    }
}
```



