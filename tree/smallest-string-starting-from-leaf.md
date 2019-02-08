# [Smallest String Starting From Leaf](https://leetcode.com/problems/smallest-string-starting-from-leaf/description/)

Given the`root`of a binary tree, each node has a value from`0`to`25`representing the letters`'a'`to`'z'`: a value of`0`represents`'a'`, a value of`1`represents`'b'`, and so on.

Find the lexicographically smallest string that starts at a leaf of this tree and ends at the root.

_\(As a reminder, any shorter prefix of a string is lexicographically smaller: for example,`"ab"`is lexicographically smaller than`"aba"`.  A leaf of a node is a node that has no children.\)_

### Example

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/01/30/tree1.png)

```
Input: 
[0,1,2,3,4,3,4]
Output: 
"dba"
```

**Example 2:**

![](https://assets.leetcode.com/uploads/2019/01/30/tree2.png)

```
Input: 
[25,1,3,1,3,0,2]
Output: 
"adz"
```

**Example 3:**

![](https://assets.leetcode.com/uploads/2019/02/01/tree3.png)

```
Input: 
[2,2,1,null,1,0,null,0]
Output: 
"abc"
```

### Note

前序遍历，注意一下退出的条件

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
    public String smallestFromLeaf(TreeNode root) {
        if (root == null) {
            return null;
        }
        char ch = (char)('a' + root.val);
        String left  = smallestFromLeaf(root.left);
        String right = smallestFromLeaf(root.right);
        if (left == null && right == null) { // leaf
            return "" + ch;
        }
        if (left == null) {
            return right + ch;
        }
        if (right == null) {
            return left + ch;
        }
        if (left.compareTo(right) < 0) {
            return left + ch;
        } else {
            return right + ch;
        }
    }
    
    
}

```



