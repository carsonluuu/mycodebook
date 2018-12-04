# [Flatten a Multilevel Doubly Linked List](https://leetcode.com/problems/flatten-a-multilevel-doubly-linked-list/description/)

You are given a doubly linked list which in addition to the next and previous pointers, it could have a child pointer, which may or may not point to a separate doubly linked list. These child lists may have one or more children of their own, and so on, to produce a multilevel data structure, as shown in the example below.

Flatten the list so that all the nodes appear in a single-level, doubly linked list. You are given the head of the first level of the list.

### **Example**

```
Input:

 1---2---3---4---5---6--NULL
         |
         7---8---9---10--NULL
             |
             11--12--NULL


Output:

1-2-3-7-8-11-12-9-10-4-5-6-NULL
```

### Note

**迭代法：**

直接改吧，找到有child的节点curr，找到这一层的tail，连到curr的后面（注意断开或者新连接都是双向的）对于不同层次的在下次会被访问，相当于level一直在减少

**递归法：**

对于链表，递归执行顺序不一样，返回第一层的时候，下面几层都已经搞好了。递归的参数往往是下一个节点。帮助函数返回必须得是tail了这里，所以需要一个帮助函数，因为主函数返回的是head。

### Code

```java
public Node flatten(Node head) {
    if (head == null) {
        return head;
    }

    Node curr = head;
    while (curr != null) {
        if (curr.child == null) {
            curr = curr.next;
            continue;
        } else {
            Node c = curr.child;
            Node next = curr.next;

            curr.next = c;
            c.prev = curr;
            while (c.next != null) {
                c = c.next;
            }
            if (next != null) {
                c.next = next;
                next.prev = c;
            }
            curr.child = null;
        }
    }

    return head;
}
```

```java
public Node flatten(Node head) {
    helper(head);
    return head;
}

private Node helper(Node head) {
    Node cur = head, pre = head;
    while(cur != null) {
        if(cur.child == null) {
            pre = cur;
            cur = cur.next;
        } else {
            Node tmp = cur.next;
            Node child = helper(cur.child);
            cur.next = cur.child;
            cur.child.prev = cur;
            cur.child = null;
            child.next = tmp;
            if (tmp != null) tmp.prev = child;
            pre = child;
            cur = tmp;
        }
    }
    return pre;
}
```



