# [Smallest Subtree with all the Deepest Nodes](https://leetcode.com/problems/smallest-subtree-with-all-the-deepest-nodes/description/)

Given a binary tree rooted at`root`, the _depth _of each node is the shortest distance to the root.

A node is _deepest _if it has the largest depth possible among any node in theentire tree.

The subtree of a node is that node, plus the set of all descendants of that node.

Return the node with the largest depth such that it contains all the deepest nodes in its subtree.

### Example

![](/assets/deepest smallest tree.png)

```
Input: [3,5,1,6,2,0,8,null,null,7,4]
Output: [2,7,4]
Explanation:

We return the node with value 2, colored in yellow in the diagram.
The nodes colored in blue are the deepest nodes of the tree.
The input "[3, 5, 1, 6, 2, 0, 8, null, null, 7, 4]" is a serialization of the given tree.
The output "[2, 7, 4]" is a serialization of the subtree rooted at the node with value 2.
Both the input and output have TreeNode type.
```

### Note

如果左右子树一样深，那么这个root就是答案

如果左子树更深，那么答案在左子树，进行递归

同理，如果右子树更深，那么答案在右子树，继续递归

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
    class ResultType {
        int depth;
        TreeNode node;
        ResultType(int depth, TreeNode node) {
            this.depth = depth;
            this.node = node;
        }
    }
    
    public TreeNode subtreeWithAllDeepest(TreeNode root) {
        if (root == null) {
            return root;
        }
        
        return helper(root).node;
    }
    
    private ResultType helper(TreeNode root) {
        if (root == null) {
            return new ResultType(0, root);
        }
        
        ResultType left  = helper(root.left);
        ResultType right = helper(root.right);
        
        if (left.depth > right.depth) {
            return new ResultType(left.depth + 1, left.node);
        }
        if (left.depth < right.depth) {
            return new ResultType(right.depth + 1, right.node);
        }
        return new ResultType(left.depth + 1, root);
        
    }
}
```



