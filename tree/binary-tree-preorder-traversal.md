# Binary Tree Preorder Traversal

遍历顺序为**根**、**左**、**右**

1. 如果根节点非空，将根节点加入到栈中。
2. 如果栈不空，弹出出栈顶节点，将其值加加入到数组中。
   1. 如果该节点的右子树不为空，将右子节点加入栈中。
   2. 如果左子节点不为空，将左子节点加入栈中。
3. 重复第二步，直到栈空。

```java
public List<Integer> preorderTraversal(TreeNode root) {
    List<Integer> res = new LinkedList<Integer>();
    if (root == null) return res;
    Stack<TreeNode> stack = new Stack<>();
    stack.push(root);
    while (!stack.isEmpty()) {
        TreeNode cur = stack.pop();
        if (cur.right != null) stack.push(cur.right);
        if (cur.left  != null) stack.push(cur.left );
        res.add(cur.val);
    }
    return res;
}
```

带parent指针的先序遍历（迭代）

![](/assets/preorderParent.png)

```java
/**
 * Definition of ParentTreeNode:
 * 
 * class ParentTreeNode {
 *     public ParentTreeNode parent, left, right;
 * }
 */

public static void printPreorder(TreeNode root) {
    TreeNode cur = root;
    while(cur != null){
        System.out.println(cur.val);

        if(cur.left != null){
            cur = cur.left;
        } else if(cur.right != null){
            cur = cur.right;
        } else {
            while(cur.parent != null && (cur.parent.right == null || cur == cur.parent.right)){
                cur = cur.parent;
            }
            if(cur.parent == null) break;
            cur = cur.parent.right;
        }
    }
}
```



