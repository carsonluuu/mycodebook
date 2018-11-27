# Binary Tree Tilt

Given a binary tree, return the tilt of the **whole tree**.

The tilt of a **tree node **is defined as the **absolute difference **between the sum of all left subtree node values and the sum of all right subtree node values. Null node has tilt 0.

The tilt of the **whole tree **is defined as the sum of all nodes' tilt.

### **Example**

```
Input:

         1
       /   \
      2     3

Output:
 1

Explanation:

Tilt of node 2 : 0
Tilt of node 3 : 0
Tilt of node 1 : |2-3| = 1
Tilt of binary tree : 0 + 0 + 1 = 1
```

### Code

```java
class Solution {
    private static class ResultType {
        int sum, diffSum;
        public ResultType(int sum, int diffSum) {
            this.sum = sum;
            this.diffSum = diffSum;
        }
    }

    public int findTilt(TreeNode root) {
        if (root == null) {
            return 0;
        }

        ResultType res = helper(root);

        return res.diffSum;
    }

    private ResultType helper(TreeNode root) {
        if (root == null) {
            return new ResultType(0, 0);
        }

        ResultType left = helper(root.left);
        ResultType right = helper(root.right);

        int diffSum = Math.abs(left.sum - right.sum) + left.diffSum + right.diffSum; 

        return new ResultType(root.val + left.sum + right.sum, diffSum);
    }
}
```



