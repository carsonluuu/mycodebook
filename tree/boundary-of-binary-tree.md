# [Boundary of Binary Tree](https://leetcode.com/problems/boundary-of-binary-tree/description/)

Given a binary tree, return the values of its boundary in **anti-clockwise **direction starting from root. Boundary includes left boundary, leaves, and right boundary in order without duplicate nodes.

**Left boundary **is defined as the path from root to the **left-most **node.**Right boundary **is defined as the path from root to the **right-most **node. If the root doesn't have left subtree or right subtree, then the root itself is left boundary or right boundary. Note this definition only applies to the input binary tree, and not applies to any subtrees.

The **left-most **node is defined as a **leaf **node you could reach when you always firstly travel to the left subtree if exists. If not, travel to the right subtree. Repeat until you reach a leaf node.

The **right-most**node is also defined by the same way with left and right exchanged.

### Example

**Example 1**

```
Input:
  1
   \
    2
   / \
  3   4

Ouput:
[1, 3, 4, 2]

Explanation:
The root doesn't have left subtree, so the root itself is left boundary.
The leaves are node 3 and 4.
The right boundary are node 1,2,4. 
Note the anti-clockwise direction means you should output reversed right boundary.
So order them in anti-clockwise without duplicates and we have [1,3,4,2].
```

**Example 2**

```
Input:
    ____1_____
   /          \
  2            3
 / \          / 
4   5        6   
   / \      / \
  7   8    9  10  
       
Ouput:
[1,2,4,7,8,9,10,6,3]

Explanation:
The left boundary are node 1,2,4. (4 is the left-most node according to definition)
The leaves are node 4,7,8,9,10.
The right boundary are node 1,3,6,10. (10 is the right-most node).
So order them in anti-clockwise without duplicate nodes we have [1,2,4,7,8,9,10,6,3].
```

### Note

注意定义，比较晦涩。left/right-most

直接暴力遍历，左边界+叶节点+右边界，其中：

1. 左边界是**前序遍历**，左孩子不为空就继续遍历左边
2. 叶子节点分别先后寻找根的左右子树，根在主函数单独先加
3. 右边界是**后序遍历**，右孩子不为空就继续遍历右边

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
    public List<Integer> boundaryOfBinaryTree(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        if (root == null) { return res; }
        
        res.add(root.val);
        addLeft(root.left, res);
        addLeave(root.left, res);
        addLeave(root.right, res);
        addRight(root.right, res);
        
        return res;
    }
    
    private void addLeft(TreeNode root, List<Integer> res) {
        if (root == null) { return; }
        if (isLeaf(root)) { return; }
        
        res.add(root.val);
        if (root.left != null) {
            addLeft(root.left, res);
        } else {
            addLeft(root.right, res);
        }
    }
    
    private void addRight(TreeNode root, List<Integer> res) {
        if (root == null) { return; }
        if (isLeaf(root)) { return; }

        if (root.right != null) {
            addRight(root.right, res);
        } else {
            addRight(root.left, res);
        }
        res.add(root.val);
    }
    
    private void addLeave(TreeNode root, List<Integer> res) {
        if (root == null) { return; }
        if (isLeaf(root)) {
            res.add(root.val);
        }
        
        addLeave(root.left, res);
        addLeave(root.right, res);
    }
    
    private boolean isLeaf(TreeNode n) {
        return n.left == null && n.right == null;
    }
}
```



