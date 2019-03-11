# [Binary Tree Upside Down](https://leetcode.com/problems/binary-tree-upside-down/)

Given a binary tree where all the right nodes are either leaf nodes with a sibling \(a left node that shares the same parent node\) or empty, flip it upside down and turn it into a tree where the original right nodes turned into left leaf nodes. Return the new root.

### **Example**

```
Input: 
[1,2,3,4,5]

    1
   / \
  2   3
 / \
4   5


Output:
 return the root of the binary tree [4,5,2,#,#,3,1]

   4
  / \
 5   2
    / \
   3   1  

```

**Clarification:**

Confused what`[4,5,2,#,#,3,1]` means? Read more below on how binary tree is serialized on OJ.

The serialization of a binary tree follows a level order traversal, where '\#' signifies a path terminator where no node exists below.

Here's an example:

```
   1
  / \
 2   3
    /
   4
    \
     5
```

The above binary tree is serialized as`[1,2,3,#,#,4,#,#,5]`.

### Note

题目比较奇怪，本质是把根的左孩子的左孩子置为根的右孩子，根的左孩子的右孩子为根，根左右都变空，对左孩子进行递归

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
    public TreeNode upsideDownBinaryTree(TreeNode root) {
        TreeNode prev = null;
        TreeNode curr = root;
        TreeNode next = null;
        TreeNode temp = null;
        
        while (curr != null) {
            next = curr.left;
            curr.left = temp;
            temp = curr.right; //for next round
            curr.right = prev;
            
            prev = curr;
            curr = next;
        }
        
        return prev;
    }
    
    public TreeNode upsideDownBinaryTree2(TreeNode root) {
        if (root == null || root.left == null) {
            return root;
        }
        
        TreeNode newNode = upsideDownBinaryTree(root.left);
        root.left.left = root.right;
        root.left.right = root;
        root.left = root.right = null;
        
        return newNode;
    }
}
```



