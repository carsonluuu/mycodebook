# [Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree/description/)

Invert a binary tree.

### **Example**

Input:

```
     4
   /   \
  2     7
 / \   / \
1   3 6   9
```

Output:

```
     4
   /   \
  7     2
 / \   / \
9   6 3   1
```

###  Note

### Code

```java
public class Solution {
    /**
     * @param root: a TreeNode, the root of the binary tree
     * @return: nothing
     */
    public void invertBinaryTree(TreeNode root) {
        if (root == null) {
            return;
        }
        TreeNode temp = root.left;
        root.left = root.right;
        root.right = temp;
        
        invertBinaryTree(root.left);
        invertBinaryTree(root.right);
    }
}
```

```java
public class Solution {
    /**
     * @param root: a TreeNode, the root of the binary tree
     * @return: nothing
     */
    public void invertBinaryTree(TreeNode root) {
        // write your code here
        if (root == null)
        {
            return;
        }
        
        Stack<TreeNode> stack = new Stack<>();
        stack.push(root);
        while(!stack.isEmpty())
        {
            TreeNode node = stack.pop();
            
            TreeNode t = node.left;
            node.left = node.right;
            node.right = t;
            
            if(node.left != null)
            {
                stack.push(node.left);
            }
            if(node.right != null)
            {
                stack.push(node.right);
            }
        }
        
    }
}
```



