# [\(FB\) BST to doubly linked-list](http://www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=175727&highlight=facebook)

LC 论坛的讨论帖[http://articles.leetcode.com/convert-binary-search-tree-bst-to/](http://articles.leetcode.com/convert-binary-search-tree-bst-to/)

### 递归

思路 ：[http://www.geeksforgeeks.org/convert-given-binary-tree-doubly-linked-list-set-3/](http://www.geeksforgeeks.org/convert-given-binary-tree-doubly-linked-list-set-3/)

* 完全就是 in - order 的递归结构，左-中-右

* 核心在于 “中” 这步上，如何正确做好 “拼接” 工作

* 我们需要存一个全局变量 prev 用于保存 "左子树的最后一个节点"，在每步上，和 root 做双向拼接； prev 初始化为 null;

* 额外用于遍历 LinkedList 还需要存下 head ; 在 prev 为 null 的时候 root 就代表着最左面的节点，设一下就好，之后就不用管了。

时间复杂度 O\(n\).

```java
private static class TreeNode{
    int val;
    TreeNode left,right;
    public TreeNode(int val){
        this.val = val;
    }
}

static TreeNode prev;
static TreeNode head;

// In-order
public static void convert(TreeNode root){
    if(root == null) return;

    convert(root.left);

    if(prev == null){
        head = root;
    } else {
        root.left = prev;
        prev.right = root;
    }
    prev = root;

    convert(root.right);

}

public static void main(String[] args){

    TreeNode node1 = new TreeNode(1);
    TreeNode node2 = new TreeNode(2);
    TreeNode node3 = new TreeNode(3);
    TreeNode node4 = new TreeNode(4);
    TreeNode node5 = new TreeNode(5);
    TreeNode node6 = new TreeNode(6);
    TreeNode node7 = new TreeNode(7);
    TreeNode node8 = new TreeNode(8);
    TreeNode node9 = new TreeNode(9);
    TreeNode node10 = new TreeNode(10);

    node2.left = node1;
    node2.right = node3;
    node4.left = node2;
    node4.right = node5;
    node6.left = node4;
    node6.right = node9;
    node9.left = node8;
    node8.left = node7;
    node9.right = node10;

    convert(node6);

    while(head != null){
        System.out.print(" " + head.val);
        head = head.right;
    }
}
```

### 迭代\(Stack\)

* In-order 跑一遍，每次 pop 出来的时候，我们就有 root 了；

* 然后拼接的逻辑处理和递归的方法完全一样，这次连全局变量都不用，简单直接~

时间O\(n\)，空间 O\(log n\)

```java
// In-order
public static TreeNode convert(TreeNode root){
    if(root == null) return null;

    TreeNode prev = null;
    TreeNode head = null;

    Stack<TreeNode> stack = new Stack<>();
    TreeNode cur = root;
    while(!stack.isEmpty() || cur != null){
        while(cur != null){
            stack.push(cur);
            cur = cur.left;
        }
        TreeNode node = stack.pop();

        if(prev == null){
            head = node;
        } else {
            prev.right = node;
            node.left = prev;
        }

        prev = node;
        cur = node.right;
    }
    return head;
}

public static void main(String[] args){

    TreeNode node1 = new TreeNode(1);
    TreeNode node2 = new TreeNode(2);
    TreeNode node3 = new TreeNode(3);
    TreeNode node4 = new TreeNode(4);
    TreeNode node5 = new TreeNode(5);
    TreeNode node6 = new TreeNode(6);
    TreeNode node7 = new TreeNode(7);
    TreeNode node8 = new TreeNode(8);
    TreeNode node9 = new TreeNode(9);
    TreeNode node10 = new TreeNode(10);

    node2.left = node1;
    node2.right = node3;
    node4.left = node2;
    node4.right = node5;
    node6.left = node4;
    node6.right = node9;
    node9.left = node8;
    node8.left = node7;
    node9.right = node10;

    TreeNode head = convert(node6);

    while(head != null){
        System.out.print(" " + head.val);
        head = head.right;
    }
}
```



