# [Find Leaves of Binary Tree](https://leetcode.com/problems/find-leaves-of-binary-tree/description/)

Given a binary tree, collect a tree's nodes as if you were doing this: Collect and remove all leaves, repeat until the tree is empty.

### **Example**

```
Input: 
[1,2,3,4,5]


          1
         / \
        2   3
       / \     
      4   5    


Output: 
[[4,5,3],[2],[1]]
```

**Explanation:**

1. Removing the leaves`[4,5,3]`would result in this tree:

```
          1
         / 
        2
```

1. Now removing the leaf`[2]`would result in this tree:

```
          1
```

1. Now removing the leaf`[1]`would result in the empty tree:

```
          []
```

### Note

利用分治，每次bottom up的时候返回当前叶子节点的高度，然后在相对应的全球数组里面开辟数组，并且往里面增值。

### Code

```java
class Solution {
    public List<List<Integer>> findLeaves(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        if (root == null) {
            return res;
        }

        helper(root, res);

        return res;
    }

    private int helper(TreeNode root, List<List<Integer>> res) {
        if (root == null) {
            return -1;
        }

        int level = 1 + Math.max(helper(root.left, res), 
                                 helper(root.right, res));
        if (res.size() == level) {
            res.add(new ArrayList<Integer>());
        }
        res.get(level).add(root.val);
        root.left = root.right = null;

        return level;
    }
}
```



