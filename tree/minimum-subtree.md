# Minimum Subtree

Given a binary tree, find the subtree with minimum sum. Return the root of the subtree.

### Example

Given a binary tree:

```
     1
   /   \
 -5     2
 / \   /  \
0   2 -4  -5
```

return the node`1`.

### Note

子树和问题，维护一个最小的全局变量

```
sum = helper(root.left) + helper(root.right) + root.val;
```

### Code

```java
public class Solution {
    /**
     * @param root: the root of binary tree
     * @return: the root of the minimum subtree
     */
    private int min = Integer.MAX_VALUE;
    private TreeNode subtree = null;

    public TreeNode findSubtree(TreeNode root) {
        helper(root);
        return subtree;
    }

    private int helper(TreeNode root) { //divide and conquer (return value)
        if (root == null) {
            return 0;
        }
        int sum = helper(root.left) + helper(root.right) + root.val;
        //post-order for divide and conquer
        if (sum <= min) {
            min = sum;
            subtree = root;
        }
        return sum;
    }
}
```



