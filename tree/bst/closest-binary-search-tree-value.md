# [Closest Binary Search Tree Value](https://leetcode.com/problems/closest-binary-search-tree-value/description/)

Given a non-empty binary search tree and a target value, find the value in the BST that is closest to the target.

**Note:**

* Given target value is a floating point.
* You are guaranteed to have only one unique value in the BST that is closest to the target.

### **Example**

```
Input:
 root = [4,2,5,1,3], target = 3.714286

    4
   / \
  2   5
 / \
1   3


Output:
 4
```

### Note

分治的做，找左边和右边

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
    public int closestValue(TreeNode root, double target) {
        if (root == null) {
            return Integer.MIN_VALUE;
        }
        if (root.val > target) {
            if (root.left != null) {
                int left = closestValue(root.left, target);
                if (Math.abs(left - target) < Math.abs(root.val - target)) {
                    return left;
                }
            }
        } else {
            if (root.right != null) {
                int right = closestValue(root.right, target);
                if (Math.abs(right - target) < Math.abs(root.val - target)) {
                    return right;
                }
            }
        }
        
        return root.val;
    }
}
```



