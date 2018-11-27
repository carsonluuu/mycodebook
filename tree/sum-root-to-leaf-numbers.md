# Sum Root to Leaf Numbers

Given a binary tree containing digits from`0-9`only, each root-to-leaf path could represent a number.

An example is the root-to-leaf path`1->2->3`which represents the number`123`.

Find the total sum of all root-to-leaf numbers.

**Note:** A leaf is a node with no children.

### **Example**

**Example 1:**

```
Input: [1,2,3]
    1
   / \
  2   3
Output: 25
Explanation:
The root-to-leaf path 1->2 represents the number 12.
The root-to-leaf path 1->3 represents the number 13.
Therefore, sum = 12 + 13 = 25.
```

**Example 2:**

```
Input: [4,9,0,5,1]
    4
   / \
  9   0
 / \
5   1
Output: 1026
Explanation:
The root-to-leaf path 4->9->5 represents the number 495.
The root-to-leaf path 4->9->1 represents the number 491.
The root-to-leaf path 4->0 represents the number 40.
Therefore, sum = 495 + 491 + 40 = 1026.
```

### Note

Divide and conquer

num是递归传递的参数

`num = num * 10 + root.val`  一直到叶子结点

### Code

```java
class Solution {
    public int sumNumbers(TreeNode root) {
        return helper(root, 0);        
    }

    private int helper(TreeNode root, int num) {
        if (root == null) {
            return 0;
        }
        num = num * 10 + root.val;

        if (root.left == null && root.right == null) {
            return num;
        }

        return helper(root.left, num) + helper(root.right, num);
    }
}
```



