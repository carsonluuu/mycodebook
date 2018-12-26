# [Trim a Binary Search Tree](https://leetcode.com/problems/trim-a-binary-search-tree/discuss/107000/Java-solution-6-liner)

Given a binary search tree and the lowest and highest boundaries as`L`and`R`, trim the tree so that all its elements lies in`[L, R]`\(R &gt;= L\). You might need to change the root of the tree, so the result should return the new root of the trimmed binary search tree.

### **Example**

**Example 1:**

```
Input:

    1
   / \
  0   2

  L = 1
  R = 2


Output:

    1
      \
       2
```

**Example 2:**

```
Input:

    3
   / \
  0   4
   \
    2
   /
  1

  L = 1
  R = 3


Output:

      3
     / 
   2   
  /
 1
```

### Note

这题做法有些取巧，并不是真正意义上在内存里面删除不符合区间的Node，只是将Node的指向进行的更改，大致思路：

每一层的Condition有三种：

1. `root.val`小于区间的lower bound`L`，则返回`root.right `subtree传上来的`root`，这里就变相的'删除'掉了当前`root`
   和所有`root.left`的node
2. `root.val`大于区间的upper bound`R`，则返回`root.left` subtree传上来的`root`
3. 满足区间，则继续递归

当递归走到叶子节点的时候，我们向上返回`root`，这里`return root`的定义是：  
返回给parent一个**区间调整完以后的subtree**

### Code

```java
class Solution {
    public TreeNode trimBST(TreeNode root, int L, int R) {
        if (root == null) return null;
        
        //每一层的Condition
        if (root.val < L) return trimBST(root.right, L, R);
        if (root.val > R) return trimBST(root.left, L, R);
        
        // 区间内，正常的Recursion
        root.left = trimBST(root.left, L, R);
        root.right = trimBST(root.right, L, R);
        
        // 返回给parent一个区间调整完以后的subtree
        return root;
    }
}
```



