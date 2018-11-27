# Lowest Common Ancestor IV

给一个 二叉树 ， 求最深节点的最小公共父节点

### Example

```
    1
   / \
  2   3
     / \
    4   5

 return 3

    1
   / \
  2   3
 /   / \
6   4   5

return 1
```

### Note

底层最左边和底层最右边的LCA  -&gt; level order

给出LCA的迭代法，关键是运用了in-order去预处理：

> 其实就是 inorder pre-process 了一遍之后，把 binary tree 当 BST 用。因为 in-order 的 index 就像 BST 里的大小一样，可以直接确定几个节点在树中的相对位置。同时因为我们都是从 root 开始一层一层往下搜索的，也能保证每次循环的 root 都一定 valid.

这个代码的优点是如果做多次 query 的话有一个 pre-processing 的缓存可以很快返回结果；缺点就是多了个 pre-processing 的过程，query 次数少的时候不占便宜。

这个代码可以 AC，基本思路就是先跑一遍 inorder traversal 记录下每个 node 在整个树里面对应的位置；利用 hashmap 对每个 node 实现均摊复杂度 O\(1\) 的查找，然后根据对应的节点 index 判断 p，q 相对于 root 在 tree 里的位置关系。

中间跑了一次迭代版的 binary tree inorder traversal.

同一个Tree上运行多次，可以采用这个方法

index of root 大于两个待找节点，root向左走

index of root 小于两个待找节点，root向右走

其他情况：处于之间，找到啦！

### Code

```java
public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
    if (root == null) return root;
    if (root.val == p.val) return p;
    if (root.val == q.val) return q;

    HashMap<TreeNode, Integer> map = new HashMap<TreeNode, Integer>();
    Stack<TreeNode> stack = new Stack<TreeNode>();

    TreeNode cur = root;
    int index = 0;
    while (cur != null || !stack.isEmpty()) {
        while(cur != null) {
            stack.push(cur);
            cur = cur.left;
        }
        TreeNode node = stack.pop();
        map.put(node, index++);
        cur = node.right;
    }

    return getLCA(root, p, q, map);
}

private TreeNode getLCA(TreeNode root, TreeNode p, TreeNode q, HashMap<TreeNode, Integer> map){
    if (root == null) return root;
    if (root.val == p.val) return p;
    if (root.val == q.val) return q;

    while (root != null) {
        if (map.get(q) < map.get(root) && map.get(p) < map.get(root)) {
            root = root.left;
        } else if (map.get(q) > map.get(root) && map.get(p) > map.get(root)) {
            root = root.right;
        } else {
            break;
        }
    }

    return root;
}
```



