# [Populating Next Right Pointers in Each Node II](https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/description/)

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

### **Example**

Given the following binary tree,

```
     1
   /  \
  2    3
 / \    \
4   5    7
```

After calling your function, the tree should look like:

```
     1 -> NULL
   /  \
  2 -> 3 -> NULL
 / \    \
4-> 5 -> 7 -> NULL

```

### Note

和之前不一样的是，这里不一定是perfect树了，所以会跨左右孩子，右连右这种情况

需要另外记一个head（这一层的第一个）和pre（前一个节点），根据这些进行连接

### Code

```java
public void connect(TreeLinkNode root) {
    TreeLinkNode cur  = root;
    TreeLinkNode pre  = null;
    TreeLinkNode head = null;
    while (cur != null) {
        while (cur != null) {
            if (cur.left != null) {
                if (pre != null) {
                    pre.next = cur.left;
                } else 
                    head = cur.left; 
                pre = cur.left;
            }
            if (cur.right != null) {
                if (pre != null) {
                    pre.next = cur.right;
                } else 
                    head = cur.right; 
                pre = cur.right;   
            }
            cur = cur.next;
        }
        cur  = head;
        pre  = null;
        head = null;
    }
}
```



