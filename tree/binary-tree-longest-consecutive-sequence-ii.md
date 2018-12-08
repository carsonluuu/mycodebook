# [Binary Tree Longest Consecutive Sequence II](https://leetcode.com/problems/binary-tree-longest-consecutive-sequence-ii/description/)

Given a binary tree, you need to find the length of Longest Consecutive Path in Binary Tree.

Especially, this path can be either increasing or decreasing. For example, \[1,2,3,4\] and \[4,3,2,1\] are both considered valid, but the path \[1,2,4,3\] is not valid. On the other hand, the path can be in the child-Parent-child order, where not necessarily be parent-child order.

**Example 1:**

```
Input:
        1
       / \
      2   3

Output: 2
Explanation: The longest consecutive path is [1, 2] or [2, 1].
```

**Example 2:**

```
Input:
        2
       / \
      1   3
Output: 3

Explanation: The longest consecutive path is [1, 2, 3] or [3, 2, 1].
```

### Note

分治法的后序遍历

与一不同的是，这里增序和降序都是可行的，而且可以拐弯，子-父-子

所以分治返回的是一个pair，取得是左右增和降的较大者。

```java
return new int[]{Math.max(left[0], right[0]), 
                 Math.max(left[1], right[1])};
```

类似的如果左或者右孩子不为空，满足当前节点和左右孩子差的绝对值为一，就使结果递增1，否则就是1

注意这里Max，拐弯的两边的增减性是相反的，要减一，左右各多取了1（base情况），因为不是边数，是节点数。

```java
max = Math.max(max, Math.max(left[0] + right[1] - 1, left[1] + right[0] - 1));
```

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
    int max = 0;
    public int longestConsecutive(TreeNode root) {
        maxTree(root);
        return max;
    }

    private int[] maxTree(TreeNode root) {
        if (root == null) return new int[2];

        int[] left  = maxTree(root.left), right = maxTree(root.right);

        if (root.left  != null && root.val == root.left.val + 1)    left[0]++;    else left[0]  = 1;
        if (root.left  != null && root.val == root.left.val - 1)    left[1]++;    else left[1]  = 1;
        if (root.right != null && root.val == root.right.val + 1)  right[0]++;    else right[0] = 1;
        if (root.right != null && root.val == root.right.val - 1)  right[1]++;    else right[1] = 1;

        max = Math.max(max, Math.max(left[0] + right[1] - 1, left[1] + right[0] - 1));

        return new int[]{Math.max(left[0], right[0]), 
                         Math.max(left[1], right[1])};
    }
}
```



