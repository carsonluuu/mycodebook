# [Recover Binary Search Tree](https://leetcode.com/problems/recover-binary-search-tree/description/)

Two elements of a binary search tree \(BST\) are swapped by mistake.

Recover the tree without changing its structure.

### Example

**Example 1:**

```
Input:
 [1,3,null,null,2]

   1
  /
 3
  \
   2


Output:
 [3,1,null,null,2]

   3
  /
 1
  \
   2

```

**Example 2:**

```
Input:
 [3,1,4,null,null,2]

  3
 / \
1   4
   /
  2


Output:
 [2,1,4,null,null,3]

  2
 / \
1   4
   /
  3
```

### Note

设置prev指针，找的条件的中序遍历前面比后面的大了，把这两个存下来，交换

### Code

```java
class Solution {
    TreeNode prev = null;
    TreeNode first = null;
    TreeNode second = null;
    public void recoverTree2(TreeNode root) {
        if (root == null) {
            return;
        }
        
        helper(root);
        int temp = first.val;
        first.val = second.val;
        second.val = temp;
    }
    
    private void helper(TreeNode root) {
        if (root == null) {
            return;
        }
        
        helper(root.left);
        if (prev != null && prev.val >= root.val) {
            if (first == null) {
                first = prev;
            }
            second = root;
        }
        prev = root;
        helper(root.right);
    }
}
```

```java
public void recoverTree(TreeNode root) {
    if (root == null) {
        return;
    }
    
    Stack<TreeNode> stack = new Stack<>();
    while (root != null) {
        stack.push(root);
        root = root.left;
    }
    
    while (!stack.isEmpty()) {  
        TreeNode node = stack.peek();
        if (prev != null && prev.val >= node.val) {
            if (first == null) {
                first = prev;
            }
            second = node;
        }
        
        prev = node;
        
        if (node.right == null) {
            node = stack.pop();
            while (!stack.isEmpty() && stack.peek().right == node) {
                node = stack.pop();
            }
        } else {
            node = node.right;
            while (node != null) {
                stack.push(node);
                node = node.left;
            }
        }
    }
    
    int temp = first.val;
    first.val = second.val;
    second.val = temp;
}
```



