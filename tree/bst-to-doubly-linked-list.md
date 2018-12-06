# [BST to doubly linked-list](http://www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=175727&highlight=facebook)

Convert a BST to a sorted circular doubly-linked list in-place. Think of the left and right pointers as synonymous to the previous and next pointers in a doubly-linked list.

Let's take the following BST as an example, it may help you understand the problem better:

![](https://assets.leetcode.com/uploads/2018/10/12/bstdlloriginalbst.png)

We want to transform this BST into a circular doubly linked list. Each node in a doubly linked list has a predecessor and successor. For a circular doubly linked list, the predecessor of the first element is the last element, and the successor of the last element is the first element.

The figure below shows the circular doubly linked list for the BST above. The "head" symbol means the node it points to is the smallest element of the linked list.

![](https://assets.leetcode.com/uploads/2018/10/12/bstdllreturndll.png)

Specifically, we want to do the transformation in place. After the transformation, the left pointer of the tree node should point to its predecessor, and the right pointer should point to its successor. We should return the pointer to the first element of the linked list.

The figure below shows the transformed BST. The solid line indicates the successor relationship, while the dashed line means the predecessor relationship.

![](https://assets.leetcode.com/uploads/2018/10/12/bstdllreturnbst.png)

### Note

**递归**

* 完全就是 in - order 的递归结构，左-中-右

* 核心在于 “中” 这步上，如何正确做好 “拼接” 工作

* 我们需要存一个全局变量 prev 用于保存 "左子树的最后一个节点"，在每步上，和 root 做双向拼接； prev 初始化为 null;

* 额外用于遍历 LinkedList 还需要存下 head ; 在 prev 为 null 的时候 root 就代表着最左面的节点，设一下就好，之后就不用管了。

时间复杂度 O\(n\).

**迭代**

* In-order 跑一遍，每次 pop 出来的时候，我们就有 root 了；

* 然后拼接的逻辑处理和递归的方法完全一样，这次连全局变量都不用，简单直接~

时间O\(n\)，空间 O\(log n\)

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public Node left;
    public Node right;

    public Node() {}

    public Node(int _val,Node _left,Node _right) {
        val = _val;
        left = _left;
        right = _right;
    }
};
*/
class Solution {
    private Node prev = null;
    public Node treeToDoublyList(Node root) {
        if (root == null) {
            return null;
        }
        Node sentinel = new Node(-99, null, null);
        prev = sentinel;
        
        helper(root);
        
        prev.right = sentinel.right;
        sentinel.right.left = prev;
        
        return sentinel.right;
        
    }
    
    private void helper(Node curr) {
        if (curr == null) {
            return;
        }
        
        helper(curr.left);
        
        prev.right = curr;
        curr.left = prev;
        prev = curr;
        
        helper(curr.right);
    }
}
```

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



