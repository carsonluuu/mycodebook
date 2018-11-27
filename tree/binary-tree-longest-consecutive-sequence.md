# Binary Tree Longest Consecutive Sequence

Given a binary tree, find the length of the longest consecutive sequence path.

The path refers to any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The longest consecutive path need to be from parent to child \(cannot be the reverse\).

### Example

**Example 1:**

```
Input:
   1
    \
     3
    / \
   2   4
        \
         5

Output: 3
Explanation: 
Longest consecutive sequence path is 
3-4-5, so return 3.
```

**Example 2:**

```
Input:
   2
    \
     3
    / 
   2    
  / 
 1

Output: 2 

Explanation: 
Longest consecutive sequence path is 2-3, not 3-2-1, so return 2.
```

### Note

这里需要一个全局变量记录最大值。

遍历或者分治都可以解决问题。

遍历：

前序遍历，需要parent指针进行prev的判断，连续就累加长度，维护res为最大的len

分治：

后序遍历，满足连续条件，根比左/右小一，则左右子树的返回值加上1，同样维护最大的len

### Code

```java
class Solution {
    private int res;
    public int longestConsecutive(TreeNode root) {
        res = 0;
        dfs(root, null, 0);

        return res;
    }

    private void dfs(TreeNode root, TreeNode parent, int len) {
        if (root == null) {
            return;
        }

        if (parent == null || parent.val + 1 == root.val) {
            len++;
        } else {
            len = 1;
        }

        res = Math.max(res, len);

        dfs(root.left,  root, len);
        dfs(root.right, root, len);
    }
}
```

```java
class Solution {
    private int res;
    public int longestConsecutive(TreeNode root) {
        res = 0;

        dfs(root);

        return res;
    }

    private int dfs(TreeNode root) {
        if (root == null) {
            return 0;
        }

        int left  = dfs(root.left);
        int right = dfs(root.right);

        int curr = 1;
        if (root.left != null && root.val + 1 == root.left.val) {
            curr = Math.max(curr, left + 1);
        }
        if (root.right != null && root.val + 1 == root.right.val) {
            curr = Math.max(curr, right + 1);
        }

        res = Math.max(res, curr);

        return curr;
    }
}
```



