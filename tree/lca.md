# Lowest Common Ancestor of a Binary Tree

Given the root and two nodes in a Binary Tree. Find the lowest common ancestor\(LCA\) of the two nodes.

The lowest common ancestor is the node with largest depth which is the ancestor of both nodes.

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

### Note

函数返回的是 "对于给定 Node 为 root 的 tree 中是否包含 p 或者 q，只要包含一个，就不返回 null 了，而我们相对于当前节点为 root 的结果，就看两边递归的 return value 决定."

在以root为根的二叉树中找A，B的LCA，如果有则返回这个LCA；如果只有其中一个就返回其中的有的那一个，都没有就null

```java
public class Solution {
    /*
     * @param root: The root of the binary search tree.
     * @param A: A TreeNode in a Binary.
     * @param B: A TreeNode in a Binary.
     * @return: Return the least common ancestor(LCA) of the two nodes.
     */
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode A, TreeNode B) {
        //root A or B (itself)
        if (root == null || root == A || root == B) {
            return root;
        }

        TreeNode left = lowestCommonAncestor(root.left, A, B);
        TreeNode right = lowestCommonAncestor(root.right, A, B);

        //left/right departed -> root
        if (left != null && right != null) {
            return root;
        }
        //only A or B return A or B
        if (left != null) {
            return left;
        }
        if (right != null) {
            return right;
        }
        //none for both
        return null;

    }
}
```

Brute Force, O\(n^2\)/O\(nlogn\)/O\(nh\)

```java
public class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null) return root;

        if (root.val == p.val) return p;
        if (root.val == q.val) return q;

        if (containsNode(root.left, p) && containsNode(root.left, q)){
            return lowestCommonAncestor(root.left, p, q);
        }
        if (containsNode(root.right, p) && containsNode(root.right, q)){
            return lowestCommonAncestor(root.right, p, q);
        }

        return root;
    }

    private boolean containsNode(TreeNode root, TreeNode node){
        if (root == null) return false;
        if (root.val == node.val) return true;

        return (containsNode(root.left, node) || containsNode(root.right, node));

    }
}
```



