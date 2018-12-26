# [Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/description/)

Given a binary tree, determine if it is a valid binary search tree \(BST\).

### Example

**Example 1:**

```
Input:

    2
   / \
  1   3

Output:
 true
```

**Example 2:**

```
    5
   / \
  1   4
     / \
    3   6

Output:
 false

Explanation:
 The input is: [5,1,4,null,null,3,6]. The root node's value is 5 but its right child's value is 4.
```

### Note

中序遍历或者分治（设置最大和最小的边界，根据现有的值的情况更新）

### Code

```java
class Solution {
    public boolean isValidBST(TreeNode root) {
        if (root == null) return true;
        return helper(root, null, null);
    }

    public boolean helper(TreeNode root, Integer min, Integer max){
        if (root == null) return true;
        if (min != null && root.val <= min) return false;
        if (max != null && root.val >= max) return false;
        return helper(root.left, min, root.val) && helper(root.right, root.val, max);
    }

    public boolean isValidBST2(TreeNode root) { //acsending order for inorder BST
       if (root == null) return true;
       Stack<TreeNode> stack = new Stack<>();
       TreeNode pre = null;
       while (root != null || !stack.isEmpty()) {
          while (root != null) {
             stack.push(root);
             root = root.left;
          }
          root = stack.pop();
          if (pre != null && root.val <= pre.val) return false; // pre is the one before root is current one 
          pre = root;
          root = root.right;
       }
       return true;
    }

}
```



