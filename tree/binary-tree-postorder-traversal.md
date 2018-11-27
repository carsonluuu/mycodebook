# Binary Tree Postorder Traversal

* post order 因为每一步用 stack 顶元素作为新的 cur，在 while 循环中只需要以 !stack.isEmpty\(\) 为条件去判断。第二点是， post-order 是【左，右，中】，压栈的时候还是先看左再看右的，顺序不能错。
* post order 遍历中最重要的是 prev 与 cur 的相对关系，相当于存了上一步的动作，用作下一步的方向。
* 用一个 stack 存着所有的 candidate node，栈顶为当前 candidate，并且以栈是否为空做唯一判断标准（还有没有要看的 candidate）

**另一种表达**：

遍历顺序为**左**、**右**、**根**

1. 如果根节点非空，将根节点加入到栈中。
2. 如果栈不空，取栈顶元素（暂时不弹出），
   1. 如果（左子树已访问过或者左子树为空），且（右子树已访问过或右子树为空），则弹出栈顶节点，将其值加入数组，
   2. 如果左子树不为空，切未访问过，则将左子节点加入栈中，并标左子树已访问过。
   3. 如果右子树不为空，切未访问过，则将右子节点加入栈中，并标右子树已访问过。
3. 重复第二步，直到栈空。

```java
//Iterative
public ArrayList<Integer> postorderTraversal(TreeNode root) {
    ArrayList<Integer> result = new ArrayList<Integer>();
    Stack<TreeNode> stack = new Stack<TreeNode>();
    TreeNode prev = null; // previously traversed node
    TreeNode curr = root;

    if (root == null) {
        return result;
    }

    stack.push(root);
    while (!stack.empty()) {
        curr = stack.peek();
        if (prev == null || prev.left == curr || prev.right == curr) { // traverse down the tree
            if (curr.left != null) {
                stack.push(curr.left);
            } else if (curr.right != null) {
                stack.push(curr.right);
            }
        } else if (curr.left == prev) { // traverse up the tree from the left
            if (curr.right != null) {
                stack.push(curr.right);
            }
        } else { // traverse up the tree from the right
            result.add(curr.val);
            stack.pop();
        }
        prev = curr;
    }

    return result;
}
```

另一种：

这种写法的主要缺点是，当 tree 非常大我们只需要输出正确结果时，reverse list 的写法必须依赖于存储所有的

* 对于给定序列 S，定义 S' 为反序序列

* 定义 R 为 root node 序列，有 R = R'

* 定义 C 为子节点序列，正确顺序为“左-右”

* 那么 post order 的序列顺序为 CR

* 如果在做pre order时生成 RC' 序列，那么反序之后可以得到 \(RC'\)' = CR' = CR = post order 序列。

```java
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        LinkedList<Integer> res = new LinkedList<>();
        if (root == null) return res;
        Stack<TreeNode> stack = new Stack<>();
        stack.push(root);
        while (!stack.isEmpty()) {
            TreeNode cur = stack.pop();
            res.addFirst(cur.val);
            if (cur.left  != null) stack.push(cur.left );
            if (cur.right != null) stack.push(cur.right);
        }
        return res;
    }
}
```



