# [Populating Next Right Pointers in Each Node](https://leetcode.com/problems/populating-next-right-pointers-in-each-node/description/)

Given a binary tree

```
struct TreeLinkNode {
  TreeLinkNode *left;
  TreeLinkNode *right;
  TreeLinkNode *next;
}
```

Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to`NULL`.

Initially, all next pointers are set to`NULL`.

**Note:**

* You may only use constant extra space.
* Recursive approach is fine, implicit stack space does not count as extra space for this problem.
* You may assume that it is a perfect binary tree \(ie, all leaves are at the same level, and every parent has two children\).

### **Example**

Given the following perfect binary tree,

```
     1
   /  \
  2    3
 / \  / \
4  5  6  7
```

After calling your function, the tree should look like:

```
     1 -> NULL
   /  \
  2 -> 3 -> NULL
 / \  / \
4->5->6->7 -> NULL
```

###  Note

主要是一层一层遍历去连结，有两种情况：

* 左右孩子相连
* 右孩子连左孩子

通过next指针可以单层从左到右走，给的是perfect树

需要注意的是需要判断一下curr的left和right是不是空，corner case是只有一个root

递归和迭代类似

### Code

```java
public void connect(TreeLinkNode root) {
    if (root == null) return;
    if (root.left != null) {
        root.left.next = root.right;
    }
    if (root.next != null && root.right != null) {
        root.right.next = root.next.left;
    }
    connect(root.left);
    connect(root.right);
}
```

```java
public void connect(TreeLinkNode root) {
    if (root == null) return;
    TreeLinkNode start = root;
    while (start != null) {
        TreeLinkNode cur = start;
        while (cur != null) {
            if (cur.left != null) {
                cur.left.next = cur.right;
            }
            if (cur.next != null && cur.right != null) {
                cur.right.next = cur.next.left;
            }
            cur = cur.next;
        }
        start = start.left;
    }
}
```



