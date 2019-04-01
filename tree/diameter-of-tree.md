# Diameter of Binary Tree

Given a binary tree, you need to compute the length of the diameter of the tree. The diameter of a binary tree is the length of the **longest **path between any two nodes in a tree. This path may or may not pass through the root.

### **Example**

Given a binary tree

```
          1
         / \
        2   3
       / \     
      4   5
```

Return **3**, which is the length of the path \[4,2,1,3\] or \[5,2,1,3\].

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
    private static class ResultType {
        int h;
        int d;
        ResultType(int h, int d) {
            this.h = h;
            this.d = d;
        }
    }
    public int diameterOfBinaryTree(TreeNode root) {
        if (root == null) {
            return 0;
        }
     
        ResultType res = dfs(root);
        
        return res.d;
    }
    
    private ResultType dfs(TreeNode root) {
        if (root == null) {
            return new ResultType(0, 0);
        }
        
        ResultType left = dfs(root.left);
        ResultType right = dfs(root.right);
        
        int h = 1 + Math.max(left.h, right.h);
        int d = Math.max(Math.max(left.d, right.d), left.h + right.h);
        
        return new ResultType(h, d);
    }
}
```



