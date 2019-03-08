# Binary Tree Inorder Traversal

遍历顺序为**左**、**根**、**右**

1. 如果根节点非空，将根节点加入到栈中。
2. 如果栈不空，取栈顶元素（暂时不弹出），
   1. 如果左子树已访问过，或者左子树为空，则弹出栈顶节点，将其值加入数组，如有右子树，将右子节点加入栈中。
   2. 如果左子树不为空，则将左子节点加入栈中。
3. 重复第二步，直到栈空。

```java
public List<Integer> inorderTraversal(TreeNode root) {
    List<Integer> res = new ArrayList<>();
    if (root == null) return res;
    Stack<TreeNode> stack = new Stack<>();
    TreeNode cur = root;
    while (cur != null || !stack.isEmpty()) {
        while (cur != null) {
            stack.push(cur);
            cur = cur.left;
        }
        cur = stack.pop();
        res.add(cur.val);
        cur = cur.right;
    }        
    return res;
}
```

更通用的解法

```java
public class Solution {
    /**
     * @param root: The root of binary tree.
     * @return: Inorder in ArrayList which contains node values.
     */
    public ArrayList<Integer> inorderTraversal(TreeNode root) {
        Stack<TreeNode> stack = new Stack<>();
        ArrayList<Integer> result = new ArrayList<>();

        while (root != null) {
            stack.push(root);
            root = root.left;
        }

        while (!stack.isEmpty()) {
            TreeNode node = stack.peek();
            result.add(node.val);

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
        return result;
    }
}
```

如果带有parent指针，另外加一个getSuccessor\(\)，然后把 root 放到二叉树最左面为起点依次调用

getSuccessor\(\) 流程，其实有点像 morris - traversal:

* 如果 cur 右子树不为空，返回右子树里面最左面的点\(也即 cur.right 一路向左最远的点\)

* 否则一路沿着\(右child - parent\) 的路线往上走，然后返回 parent 就行了

```java
public static void printInorder(TreeNode root) {
     TreeNode cur = root;
     while(cur.left != null){
         cur = cur.left;
     }
     // Now current is at left most pos
     while(cur != null){
         System.out.println(cur.val);
         cur = getSuccessor(cur);
     }
 }

 private static TreeNode getSuccessor(TreeNode cur){
     // Find leftmost node in right subtree
     if(cur.right != null){
         cur = cur.right;
         while(cur.left != null) cur = cur.left;
     } else {
     //
         while(cur.parent != null && cur == cur.parent.right){
             cur = cur.parent;
         }
         if(cur.parent == null) return null;

         cur = cur.parent;
     }
     return cur;
 }
```

迭代器版本

```java
/**
 * Definition for binary tree
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */

public class BSTIterator {
    private TreeNode cur;
    private Stack<TreeNode> stack;
    
    public BSTIterator(TreeNode root) {
        cur = root;
        stack = new Stack<>();
    }

    /** @return whether we have a next smallest number */
    public boolean hasNext() {
        return (cur != null || !stack.isEmpty());
    }

    /** @return the next smallest number */
    public int next() {
        while (cur != null) {
            stack.push(cur);
            cur = cur.left;
        }
        cur = stack.pop();
        int val = cur.val;
        cur = cur.right;
        return val;
    }
}

/**
 * Your BSTIterator will be called like this:
 * BSTIterator i = new BSTIterator(root);
 * while (i.hasNext()) v[f()] = i.next();
 */
```



