# LinkedList

* ### Design

> [https://leetcode.com/problems/design-linked-list/description/](https://leetcode.com/problems/design-linked-list/description/)

* ### Reverse

```java
public ListNode reverseList(ListNode head) {
    /* iterative solution */
    ListNode prev = null;
    while (head != null) {
        ListNode next = head.next;
        head.next = prev;
        prev = head;
        head = next;
    }
    return prev;
}

public ListNode reverseList(ListNode head) {
    /* recursive solution */
    return reverseListInt(head, null);
}

private ListNode reverseListInt(ListNode prev, ListNode head) {
    if (head == null)
        return prev;
    ListNode next = head.next;
    head.next = prev;
    return reverseListInt(head, next);
}
```

\*Reverse for an interval \[m, n\]

![](/assets/reverseLinkedList2.png)

```java
class Solution {
    public ListNode reverseBetween(ListNode head, int m, int n) {
        ListNode sentinel = new ListNode(-99);
        sentinel.next = head;
        ListNode pre = sentinel;
        ListNode cur = sentinel.next;
        for (int i = 1; i < m; i++) {
            cur = cur.next;
            pre = pre.next;
        }
        for (int i = 0; i < n - m; i++) {
            ListNode next = cur.next;
            cur.next = next.next;
            next.next = pre.next;
            pre.next = next;
        }
        return sentinel.next;
    }
}
```

* ### Insert

```java
public ListNode insertNode(ListNode head, int val) {
    // write your code here
    ListNode node = new ListNode(val);
    if (head == null) return node;

    ListNode dummy = new ListNode(-99);
    dummy.next = head;
    head = dummy;

    while (head.next != null && head.next.val < val) {
        head = head.next;
    }

    node.next = head.next;
    head.next = node;

    return dummy.next;
}
```

* ### Delete

Remove Nth Node From End of List

```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode sentinel = new ListNode(0);
        sentinel.next = head;

        ListNode slow = sentinel;
        ListNode fast = sentinel;

        // the diff of fast and slow is n
        for (int i = 0; i < n; i++) {
            fast = fast.next;
        }

        while (fast.next != null) {
            slow = slow.next;
            fast = fast.next;
        }

        slow.next = slow.next.next;

        return sentinel.next;
    }
}
```

Remove Linked List Elements

\(注意下没准要删除的元素是连续的，那种情况下不要动 head\)

```java
class Solution {
    public ListNode removeElements(ListNode head, int val) {
        if (head == null) return null;
        ListNode sentinel = new ListNode(-99);
        sentinel.next = head;
        ListNode cur = sentinel; //prev
        while (cur.next != null) {
            if (cur.next.val == val) {
                head = head.next;
                cur.next = head;
            } else {
                cur = cur.next;
                head = head.next;
            }
        }

        return sentinel.next;
    }
}
```

Delete Node in a Linked List

\(Shift the elements after the deleted one\)

```java
class Solution {
    public void deleteNode(ListNode node) {
        ListNode sentinel = new ListNode(0);
        sentinel.next = node;
        while (node.next != null) {
            sentinel.next.val = node.next.val;
            sentinel = node;
            node = node.next;
        }

        sentinel.next = null;
    }
}
```

Remove Duplicates from Sorted List

```java
public class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        while (head != null && head.next != null) {
            if (head.val == head.next.val) {
                head.next = head.next.next;
            } else {
                head = head.next;
            }
        }

        return dummy.next;
    }
}
```

* ### Swap

Swap Nodes in Pairs

```java
class Solution {
    public ListNode swapPairs(ListNode head) {
        if (head == null || head.next == null) return head;
        ListNode sentinel = new ListNode(-99);
        sentinel.next = head;

        ListNode l1 = sentinel;
        ListNode l2 = head;
        while (l2 != null && l2.next != null) {
            ListNode nextStart = l2.next.next;

            l1.next = l2.next;
            l2.next.next = l2;
            l2.next = nextStart;

            l1 = l2;
            l2 = l1.next;
        }
        return sentinel.next;
    }
}
```

Odd Even Linked List \(odd place ones first, then even ones\)

```java
class Solution {
    public ListNode oddEvenList(ListNode head) {
        if (head == null || head.next == null) return head;
        ListNode odd= head, even = head.next;
        ListNode evenHead = even; // record even's head
        while (even != null && even.next != null) {
            odd.next = even.next;
            odd = odd.next;
            even.next = odd.next;
            even = even.next;
        }
        odd.next = evenHead;
        return head;
    }
}
```

* ### Merge \(Sorted\)

```java
public class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(0);
        ListNode head = dummy;

        while(l1 != null && l2 != null){
            if(l1.val < l2.val){
                head.next = l1;
                l1 = l1.next;
            } else {
                head.next = l2;
                l2 = l2.next;
            }
            head = head.next;
        }
        while(l1 != null){
            head.next = l1;
            l1 = l1.next;
            head = head.next;
        }
        while(l2 != null){
            head.next = l2;
            l2 = l2.next;
            head = head.next;
        }

        return dummy.next;
    }
}
```

```java
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if (l1 == null) {
            return l2;
        }
        else if (l2 == null) {
            return l1;
        }
        else if (l1.val < l2.val) {
            l1.next = mergeTwoLists(l1.next, l2);
            return l1;
        }
        else {
            l2.next = mergeTwoLists(l1, l2.next);
            return l2;
        }

    }
}
```

* ### Middle

```java
public ListNode findMiddle(ListNode head) { // second one
    ListNode slow = head;
    ListNode fast = head;
    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
    }
    return slow;        
}
```

```java
public ListNode findMiddle(ListNode head) { // first one
    if (head == null || head.next == null) {
        return head;
    }

    ListNode fast = head.next, slow = head;
    while (fast != null && fast.next != null) {
        fast = fast.next.next;
        slow = slow.next;
    }
    return slow;
}
```

* ### Reverse Print

```java
private static void reversePrintList_recursive(ListNode head){
    if(head.next == null){
        System.out.print(head.val + ",");
        return;
    }
    reversePrintList_recursive(head.next);
    System.out.print(head.val + ",");
}

private static void reversePrintList_iterative(ListNode head){
    int size = 0;
    ListNode cur = head;
    while(cur != null){
        size++;
        cur = cur.next;
    }

    for(; size > 0; size --){
        ListNode ptr = head;
        for(int i = 0; i < size - 1; i++) ptr = ptr.next;
        System.out.print(ptr.val + ",");
    }
}
```



