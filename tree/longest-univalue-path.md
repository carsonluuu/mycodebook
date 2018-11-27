# [Longest Univalue Path](https://leetcode.com/problems/longest-univalue-path/description/)

Given a binary tree, find the length of the longest path where each node in the path has the same value. This path may or may not pass through the root.

**Note:**The length of path between two nodes is represented by the number of edges between them.

**Example 1:**

```
              5
             / \
            4   5
           / \   \
          1   1   5
```

Output:

```
2
```

**Example 2:**

```
              1
             / \
            4   5
           / \   \
          4   4   5
```

Output:

```
2
```

### Note

分治

路径长是左加右，如果当前节点和左或者右的大小相同，那么左右递归的结果要加上1，记录为左右的res。

出现null值时直接归零，结果是左右的res的和

### Code

```java
class Solution {
    public int longestUnivaluePath(TreeNode root) {
        int[] res = new int[1];
        if (root != null) dfs(root, res);
        return res[0];
    }

    private int dfs(TreeNode node, int[] res) {
        int l = node.left != null ? dfs(node.left, res) : 0; 
        // Longest-Univalue-Path-Start-At - left child
        int r = node.right != null ? dfs(node.right, res) : 0; 
        // Longest-Univalue-Path-Start-At - right child
        int resl = node.left != null && node.left.val == node.val ? l + 1 : 0; 
        // Longest-Univalue-Path-Start-At - node, and go left
        int resr = node.right != null && node.right.val == node.val ? r + 1 : 0; 
        // Longest-Univalue-Path-Start-At - node, and go right
        res[0] = Math.max(res[0], resl + resr); // Longest-Univalue-Path-Across - node
        return Math.max(resl, resr);
    }
}
```



