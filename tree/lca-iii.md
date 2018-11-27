# Lowest Common Ancestor III

Given the root and two nodes in a Binary Tree. Find the lowest common ancestor\(LCA\) of the two nodes.  
The lowest common ancestor is the node with largest depth which is the ancestor of both nodes.  
Return`null`if LCA does not exist.

### Example

For the following binary tree:

```
  4
 / \
3   7
   / \
  5   6
```

LCA\(3, 5\) =`4`

LCA\(5, 6\) =`7`

LCA\(6, 7\) =`7`

node A or node B may not exist in tree.

### Note

需要ResultType来记录a存不存在，b存不存在。

> boolean a\_exist = left\_rt.a\_exist \|\| right\_rt.a\_exist \|\| A == root;
>
>         boolean b\_exist = left\_rt.b\_exist \|\| right\_rt.b\_exist \|\| B == root;

结果要求左右都存在

### Code

```java
/**
 * Definition of TreeNode:
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left, right;
 *     public TreeNode(int val) {
 *         this.val = val;
 *         this.left = this.right = null;
 *     }
 * }
 */


public class Solution {
    class ResultType {
        public boolean a_exist, b_exist;
        public TreeNode node;
        public ResultType(boolean a_exist, boolean b_exist, TreeNode node) {
            this.a_exist = a_exist;
            this.b_exist = b_exist;
            this.node = node;
        }
    }
    /*
     * @param root: The root of the binary tree.
     * @param A: A TreeNode
     * @param B: A TreeNode
     * @return: Return the LCA of the two nodes.
     */
    public TreeNode lowestCommonAncestor3(TreeNode root, TreeNode A, TreeNode B) {
        // write your code here
        ResultType res = helper(root, A, B);
        
        if (res.a_exist && res.b_exist) {
            return res.node;
        } else {
            return null;
        }
    }
    
    private ResultType helper(TreeNode root, TreeNode A, TreeNode B) {
        if (root == null) {
            return new ResultType(false, false, null);
        }
        
        ResultType left_rt = helper(root.left, A, B);
        ResultType right_rt = helper(root.right, A, B);
        
        boolean a_exist = left_rt.a_exist || right_rt.a_exist || A == root;
        boolean b_exist = left_rt.b_exist || right_rt.b_exist || B == root;
        
        if (root == A || root == B) {
            return new ResultType(a_exist, b_exist, root);
        }
        
        if (left_rt.node != null && right_rt.node != null) {
            return new ResultType(a_exist, b_exist, root);
        }
        
        if (left_rt.node != null) {
            return new ResultType(a_exist, b_exist, left_rt.node);
        }
        
        if (right_rt.node != null) {
            return new ResultType(a_exist, b_exist, right_rt.node);
        }
        
        return new ResultType(a_exist, b_exist, null);
    }
}
```



