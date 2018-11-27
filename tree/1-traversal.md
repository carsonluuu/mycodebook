# 二叉树上的遍历法

### 定义

遍历（Traversal），顾名思义，就是`通过某种顺序，一个一个访问一个数据结构中的元素`。比如我们如果需要遍历一个数组，无非就是要么从前往后，要么从后往前遍历。但是对于一棵二叉树来说，他就有很多种方式进行遍历：

1. 层序遍历（Level order）
2. 先序遍历（Pre order）
3. 中序遍历（In order）
4. 后序遍历（Post order）

我们在之前的课程中，已经学习过了二叉树的层序遍历，也就是使用 BFS 算法来获得二叉树的分层信息。通过 BFS 获得的顺序我们也可以称之为 BFS Order。而剩下的三种遍历，都需要通过深度优先搜索的方式来获得。而这一小节中，我们将讲一下通过深度优先搜索（DFS）来获得的节点顺序，

### 先序遍历 / 中序遍历 / 后序遍历

#### 先序遍历（又叫先根遍历、前序遍历）

首先访问根结点，然后遍历左子树，最后遍历右子树。**遍历左、右子树时，仍按先序遍历**。若二叉树为空则返回。

该过程可简记为**根左右**，注意该过程是**递归的**。如图先序遍历结果是：**ABDECF**。  
![](http://media.jiuzhang.com/markdown/images/3/15/d77b07ce-27f7-11e8-9f14-0242ac110002.jpg "图片")  
核心代码：

```java
// 将根作为root，空ArrayList作为result传入，即可得到整棵树的遍历结果
private void traverse(TreeNode root, ArrayList<Integer> result) {
    if (root == null) {
        return;
    }
    result.add(root.val);
    traverse(root.left, result);
    traverse(root.right, result);
}
```

#### 中序遍历（又叫中根遍历）

首先遍历左子树，然后访问根结点，最后遍历右子树。**遍历左、右子树时，仍按中序遍历**。若二叉树为空则返回。简记为**左根右**。  
上图中序遍历结果是：**DBEAFC**。  
核心代码：

```java
private void traverse(TreeNode root, ArrayList<Integer> result) {
    if (root == null) {
        return;
    }
    traverse(root.left, result);
    result.add(root.val);  // 注意访问根节点放到了遍历左子树的后面
    traverse(root.right, result);
}
```

#### 后序遍历（又叫后根遍历）

首先遍历左子树，然后遍历右子树，最后访问根结点。**遍历左、右子树时，仍按后序遍历**。若二叉树为空则返回。简记为**左右根**。  
上图后序遍历结果是：**DEBFCA**。  
核心代码：

```java
private void traverse(TreeNode root, ArrayList<Integer> result) {
    if (root == null) {
        return;
    }
    traverse(root.left, result);
    traverse(root.right, result);
    result.add(root.val);  // 注意访问根节点放到了最后
}
```

### 一些有趣的题目：

[http://www.lintcode.com/problem/construct-binary-tree-from-inorder-and-postorder-traversal/](http://www.lintcode.com/problem/construct-binary-tree-from-inorder-and-postorder-traversal/)  
[http://www.lintcode.com/problem/construct-binary-tree-from-preorder-and-inorder-traversal/](http://www.lintcode.com/problem/construct-binary-tree-from-preorder-and-inorder-traversal/)

