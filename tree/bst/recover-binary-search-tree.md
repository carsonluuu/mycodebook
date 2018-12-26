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
public class Solution {
    /**
     * @param root: the given tree
     * @return: the tree after swapping
     */
    public TreeNode bstSwappedNode(TreeNode root) {
        // write your code here
        if (root == null) {
            return null;
        }
        
        TreeNode swapNode1 = null, swapNode2 = null;
        Stack<TreeNode> stack = new Stack<>();
        TreeNode p = root, last = null;
        while (!stack.isEmpty() || p != null) {
            while (p != null) {
                stack.push(p);
                p = p.left;
            }
            p = stack.pop();
            // swap judge
            if (last != null && p.val < last.val) {
                if (swapNode1 == null && swapNode2 == null) {
                    // 第一次触法exchange judge，last是swapNode
                    // 此外，中序相邻点交换会使得 exchange judge 只触法一次
                    swapNode1 = last;
                    swapNode2 = p;  // 避免额外判定
                } else {
                    // 第二次触法exchange judge，p是swapNode
                    swapNode2 = p;
                    break;
                }
            }
            last = p;
            p = p.right;
        }

        // swap
        if (swapNode1 != null && swapNode2 != null) {
            int tmp = swapNode1.val;
            swapNode1.val = swapNode2.val;
            swapNode2.val = tmp;
        }
        
        return root;
    }
}
```



