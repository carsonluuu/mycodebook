# Subtree with Maximum Average

Given a binary tree, find the subtree with maximum average. Return the root of the subtree.

### Example

Given a binary tree:

```
     1
   /   \
 -5     11
 / \   /  \
1   2 4    -2
```

return the node`11`.

### Note

最好把sum和size都记下来

sumA/sizeA   &gt;  sumB/sizeB比较可以化作 sumA \* sizeB   &gt;  sumB \* sizeA

如果用除法的话, size为0无意义, 而且精度有流失

### Code

```java
public class Solution {
    private class ResultType {
        public int sum, size;
        public ResultType(int sum, int size) {
            this.sum = sum;
            this.size = size;
        }
    }

    private TreeNode subtree = null;
    private ResultType subtreeResult = null;

    /**
     * @param root: the root of binary tree
     * @return: the root of the maximum average of subtree
     */
    public TreeNode findSubtree2(TreeNode root) {
        // write your code here
        helper(root);
        return subtree;
    }

    private ResultType helper(TreeNode root) {
        if (root == null) {
            return new ResultType(0, 0);
        }
        ResultType left = helper(root.left);
        ResultType right = helper(root.right);

        ResultType result = new ResultType(
            left.sum + right.sum + root.val,
            left.size + right.size + 1
        );

        if (subtree == null || 
            subtreeResult.sum * result.size < 
            result.sum * subtreeResult.size) {
            subtree = root;
            subtreeResult = result;
        }
        return result;

    }
}
```



