# [Balanced Binary Tree](/tree/balanced-binary-tree.md)

Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as:

> a binary tree in which the depth of the two subtrees of\_every\_node never differ by more than 1.

### Example

**Example 1:**

Given the following tree`[3,9,20,null,null,15,7]`:

```
    3
   / \
  9  20
    /  \
   15   7
```

Return true.

**Example 2:**

Given the following tree`[1,2,2,3,3,null,null,4,4]`:

```
       1
      / \
     2   2
    / \
   3   3
  / \
 4   4
```

Return false.

### Note

We can use ResultType to return two parameter in terms of the recursion

```
class ResultType {
    public boolean isBalanced;
    public int maxDepth;
    public ResultType(boolean isBalanced, int maxDepth) {
        this.isBalanced = isBalanced;
        this.maxDepth = maxDepth;
    }
}
```

Or we can use -1 to denote that the subtree/tree is not balanced

### Code

```java
public class Solution {
    public boolean isBalanced(TreeNode root) {
        return maxDepth(root) != -1;
    }

    private int maxDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }

        int left = maxDepth(root.left);
        int right = maxDepth(root.right);
        if (left == -1 || right == -1 || Math.abs(left-right) > 1) {
            return -1;
        }
        return Math.max(left, right) + 1;
    }
}
```

```java
public class Solution {
    /**
     * @param root: The root of binary tree.
     * @return: True if this Binary tree is Balanced, or false.
     */
    public boolean isBalanced(TreeNode root) {
        return helper(root).isBalanced;
    }

    private ResultType helper(TreeNode root) {
        if (root == null) {
            return new ResultType(true, 0);
        }

        ResultType left = helper(root.left);
        ResultType right = helper(root.right);

        // subtree not balance
        if (!left.isBalanced || !right.isBalanced) {
            return new ResultType(false, -1);
        }

        // root not balance
        if (Math.abs(left.maxDepth - right.maxDepth) > 1) {
            return new ResultType(false, -1);
        }

        return new ResultType(true, Math.max(left.maxDepth, right.maxDepth) + 1);
    }
}
```

```java
//O(n^2) Brute Force
public class Solution {
    public boolean isBalanced(TreeNode root) {
        if (root == null) return true;

        int lh = getHeight(root.left);
        int rh = getHeight(root.right);

        if (Math.abs(lh - rh) > 1) {
            return false;
        }

        return (isBalanced(root.left) && isBalanced(root.right));
    }

    private int getHeight(TreeNode node) {
        if (node == null) return 0;

        int lh = getHeight(node.left);
        int rh = getHeight(node.right);

        return Math.max(lh, rh) + 1;
    }
}
```



