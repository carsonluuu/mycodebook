# [Find Mode in Binary Search Tree](https://leetcode.com/problems/find-mode-in-binary-search-tree/description/)

Given a binary search tree \(BST\) with duplicates, find all the [mode\(s\)](https://en.wikipedia.org/wiki/Mode_%28statistics%29) \(the most frequently occurred element\) in the given BST.

Assume a BST is defined as follows:

* The left subtree of a node contains only nodes with keys **less than or equal to **the node's key.
* The right subtree of a node contains only nodes with keys **greater than or equal to **the node's key.
* Both the left and right subtrees must also be binary search trees.

For example:  
Given BST`[1,null,2,2]`,

```
   1
    \
     2
    /
   2
```

return`[2]`.

**Note: **If a tree has more than one mode, you can return them in any order.

### Note

中序遍历，众数可能不是唯一的

### Code

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public int[] findMode(TreeNode root) {
        List<Integer> ans = new ArrayList<>();
        TreeNode prev = null;
        int max = 0, freq = 0;
        Stack<TreeNode> stack = new Stack<>();
        TreeNode curr = root;
        while (curr != null || !stack.isEmpty()) {
            while (curr != null) {
                stack.push(curr);
                curr = curr.left;
            }
            curr = stack.pop();
            if (prev != null && curr.val == prev.val) {
                freq++;
            } else {
                freq = 1;
            }

            if (max == freq) {
                ans.add(curr.val);
            } else if (freq > max) {
                max = freq;
                ans = new ArrayList<>();
                ans.add(curr.val);
            }
            prev = curr;
            curr = curr.right;
        }

        int[] res = new int[ans.size()];
        for (int i = 0; i < res.length; i++) res[i] = ans.get(i);
        return res;
    }
}
```

```java
public class Solution {
    List<Integer> ans = new ArrayList<>();
    Integer pre;
    int maxFreq = 0, curFreq = 0;
    public int[] findMode(TreeNode root) {
        traverse(root);
        int[] res = new int[ans.size()];
        for (int i = 0; i < res.length; i++) res[i] = ans.get(i);
        return res;
    }

    private void traverse(TreeNode root) {
        if (root == null) {
            return;
        }
        //inorder traversal
        traverse(root.left);
        if (pre != null && root.val == pre) {
            curFreq++;
        } else {
            curFreq = 1;
        }
        if (curFreq == maxFreq) {
            ans.add(root.val);
        } else if (curFreq > maxFreq) {
            maxFreq = curFreq;
            ans = new ArrayList<>();
            ans.add(root.val);
        } 

        pre = root.val;
        traverse(root.right);
    }
}
```



