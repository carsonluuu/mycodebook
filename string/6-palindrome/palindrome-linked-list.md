# [Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/description/)

Given a singly linked list, determine if it is a palindrome.

### Example

**Example 1:**

```
Input:
 1->2

Output:
 false
```

**Example 2:**

```
Input:
 1->2->2->1

Output:
 true
```

**Follow up:**  
Could you do it in O\(n\) time and O\(1\) space?

### Note

找中点+reverse+两个头指针比较

### Code

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public boolean isPalindrome(ListNode head) {
        if(head == null || head.next == null) return true;
        // if(head.next.next == null && head.val != head.next.val)
        //     return false;
        ListNode middle = findMiddle(head);
        ListNode p = head;
        ListNode q = reverse(middle);
        while (q != null) {
            if (q.val != p.val)
                return false;
            q = q.next;
            p = p.next;
        }
        return true;
    }
    
    public ListNode findMiddle(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;        
    }
    
    public ListNode reverse(ListNode head) {
        ListNode prev = null;
        while (head != null) {
            ListNode temp = head.next;
            head.next = prev;
            prev = head;
            head = temp;
        }
        return prev;
    }
}
```



