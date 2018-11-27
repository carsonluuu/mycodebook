# Binary Tree Paths

Given a binary tree, return all root-to-leaf paths.

### Example

Given the following binary tree:

```
   1
 /   \
2     3
 \
  5
```

All root-to-leaf paths are:

```
[
  "1->2->5",
  "1->3"
]
```

### Code

```java
public class Solution {
    /**
     * @param root: the root of the binary tree
     * @return: all root-to-leaf paths
     */
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> res = new ArrayList<>();
        if (root == null) {
            return res;
        }
        helper(root, String.valueOf(root.val), res);
        return res;
    }

    private void helper(TreeNode root, String path, List<String> res) {
        if (root == null) {
            return;
        }
        if (root.left == null && root.right == null) {
            res.add(path);
        }
        //backtracking
        if (root.left != null) {
            helper(root.left, path + "->" + root.left.val, res);
            //                ---------------------------
        }
        if (root.right != null) {
            helper(root.right, path + "->" + root.right.val, res);
        }
    } 
}
```

```java
//Divide and Conquer
//Not that easy to understand
public List<String> binaryTreePaths(TreeNode root) {
    List<String> paths = new ArrayList<>();
    if (root == null) {
        return paths;
    }

    // root is a leaf
    if (root.left == null && root.right == null) {
        paths.add("" + root.val);
    }

    List<String> leftPaths = binaryTreePaths(root.left);
    List<String> rightPaths = binaryTreePaths(root.right);
    for (String path : leftPaths) {
        paths.add(root.val + "->" + path);
    }
    for (String path : rightPaths) {
        paths.add(root.val + "->" + path);
    }

    return paths;
}
```



