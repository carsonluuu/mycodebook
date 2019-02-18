# [Cousins in Binary Tree](https://leetcode.com/problems/cousins-in-binary-tree/description/)

In a binary tree, the root node is at depth`0`, and children of each depth`k`node are at depth`k+1`.

Two nodes of a binary tree are_cousins_if they have the same depth, but have **different parents**.

We are given the`root`of a binary tree with unique values, and the values`x` and`y` of two different nodes in the tree.

Return `true` if and only if the nodes corresponding to the values`x`and`y`are cousins.



**Example 1:  
**![](https://assets.leetcode.com/uploads/2019/02/12/q1248-01.png)

```
Input: 
root = 
[1,2,3,4]
, x = 
4
, y = 
3
Output: 
false
```

**Example 2:  
**![](https://assets.leetcode.com/uploads/2019/02/12/q1248-02.png)

```
Input: 
root = 
[1,2,3,null,4,null,5]
, x = 
5
, y = 
4
Output: 
true
```

**Example 3:**

![](https://assets.leetcode.com/uploads/2019/02/13/q1248-03.png)

```
Input: 
root = 
[1,2,3,null,4]
, x = 2, y = 3

Output: 
false
```



### Note

直接暴力做吧，依据：深度一样，parent不一样，分别存一下吧



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
    Map<Integer, TreeNode> parent = new HashMap<>(); // key: val of node, val: parent node
    Map<Integer, Integer> depth = new HashMap<>(); // key: val of node, val: depth
    public boolean isCousins(TreeNode root, int x, int y) {
        dfs(root, null);
        return depth.get(x) == depth.get(y) && parent.get(x) != parent.get(y);
    }
    
    private void dfs(TreeNode root, TreeNode par) {
        if (root == null) {
            return;
        }
        parent.put(root.val, par);
        depth.put(root.val, par == null ? 0 : 1 + depth.get(par.val));
        dfs(root.left, root);
        dfs(root.right, root);
    }
}
```

  


