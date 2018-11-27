# Same/Symmetric Tree

Given two binary trees, write a function to check if they are the same or not.

Two binary trees are considered the same if they are structurally identical and the nodes have the same value.

**Same**

**Example 1:**

```
Input:     1         1
          / \       / \
         2   3     2   3

        [1,2,3],   [1,2,3]

Output: true
```

**Example 2:**

```
Input:     1         1
          /           \
         2             2

        [1,2],     [1,null,2]

Output: false
```

**Example 3:**

```
Input:     1         1
          / \       / \
         2   1     1   2

        [1,2,1],   [1,1,2]

Output: false
```

**Symmetric**

Given a binary tree, check whether it is a mirror of itself \(ie, symmetric around its center\).

For example, this binary tree`[1,2,2,3,4,4,3]`is symmetric:

```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```

But the following`[1,2,2,null,3,null,3]`is not:

```
    1
   / \
  2   2
   \   \
   3    3
```

### Node

Double pre-order

```
isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
```

```java
isSymmetric(p.left, q.right) && isSymmetric(p.right, q.left);
```

### Code

```java
class Solution {
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if (p == null && q == null) return true;
        if (p == null || q == null) return false;
        if (p.val != q.val) return false;

        return isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
    }
}
```

```java
class Solution {
    public boolean isSymmetric(TreeNode root) {
        if (root == null) return true;
        return helper(root.left, root.right);
    }

    public static boolean helper(TreeNode p, TreeNode q){
        if (p == null && q == null) return true;
        if (p == null || q == null) return false;
        if (p.val != q.val) return false;
        return helper(p.left, q.right) && helper(p.right, q.left);
    }
}
```



