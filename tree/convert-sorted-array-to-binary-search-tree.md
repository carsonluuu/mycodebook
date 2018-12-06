# [Convert Sorted List to Binary Search Tree](https://leetcode.com/problems/convert-sorted-list-to-binary-search-tree/description/)

Given an array where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of_every_node never differ by more than 1.

### **Example**

```
Given the sorted array: [-10,-3,0,5,9],

One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:

      0
     / \
   -3   9
   /   /
 -10  5
```

### Note

两种input，要么是原生数组/列表，要么是链表。链表要麻烦一些

本质还是寻找中点，divide and conquer左右两边

base case：left &gt; right: return null

### Code

```java
class Solution {
    public TreeNode sortedArrayToBST(int[] nums) {
        if (nums == null || nums.length == 0) return null;
        return helper(nums, 0, nums.length - 1);
    }
    
    public TreeNode helper(int[] nums, int left, int right) {
        if (left > right) return null;
        int mid = (right - left) / 2 + left;
        TreeNode node = new TreeNode(nums[mid]);
        node.left  = helper(nums, left,    mid - 1);
        node.right = helper(nums, mid + 1, right);
        return node;
    }
```

```java
class Solution {
    public TreeNode sortedListToBST(ListNode head) {
        if (head == null) return null;
        return helper(head, null);
    }
    
    public TreeNode helper(ListNode head, ListNode tail) {
        if (head == tail) return null;        
        
        ListNode slow = head;
        ListNode fast = head;
        
        while (fast != tail && fast.next != tail){
            fast = fast.next.next;
            slow = slow.next;
        }

        TreeNode node = new TreeNode(slow.val);
        node.left  = helper(head, slow);
        node.right = helper(slow.next, tail);
        return node;
    }
}
```



