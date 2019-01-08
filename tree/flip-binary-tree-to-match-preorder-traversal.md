# [Flip Binary Tree To Match Preorder Traversal](https://leetcode.com/problems/flip-binary-tree-to-match-preorder-traversal/discuss/214216/JavaC++Python-DFS-Solution)

Given a binary tree with`N`nodes, each node has a different value from `{1, ..., N}`.

A node in this binary tree can be _flipped_ by swapping the left child and the right child of that node.

Consider the sequence of `N`values reported by a preorder traversal starting from the root.  Call such a sequence of`N`values the _voyage_ of the tree.

\(Recall that a_preorder traversal_ of a node means we report the current node's value, then preorder-traverse the left child, then preorder-traverse the right child.\)

Our goal is to flip the **least number **of nodes in the tree so that the voyage of the tree matches the`voyage`we are given.

If we can do so, then return a list of the values of all nodes flipped.  You may return the answer in any order.

If we cannot do so, then return the list`[-1]`.

### Example

**Example 1:**

```
Input: 
root = [1,2], voyage = [2,1]
Output: 
[-1]
```

**Example 2:**

```
Input: 
root = [1,2,3], voyage = [1,3,2]
Output: 
[1]
```

**Example 3:**

```
Input: 
root = [1,2,3], voyage = [1,2,3]
Output: 
[]
```

### Note

逻辑就是进行前序遍历树，同时遍历数组，在相等的遇到不相等的左孩子，就反转，然后递归，如果遇到不相等的情况，就直接返回false

### Code

```java
public List<Integer> flipMatchVoyage(TreeNode root, int[] voyage) {
    List<Integer> res = new ArrayList<>();
    int i = 0;
    Stack<TreeNode> s = new Stack<>();
    s.push(root);
    while (!s.isEmpty()) {
        TreeNode curr = s.pop();
        if (curr == null) { continue; }
        if (curr.val != voyage[i++]) { return Arrays.asList(-1); }
        if (curr.right != null && curr.right.val == voyage[i]) {
            if (curr.left != null) {
                res.add(curr.val);
            }
            s.push(curr.left);
            s.push(curr.right);
        } else {
            s.push(curr.right);
            s.push(curr.left);
        }
    }
    
    return res;
}
```

```java
List<Integer> res = new ArrayList<>();
int i = 0;
public List<Integer> flipMatchVoyage(TreeNode root, int[] voyage) {
    if (dfs(root, voyage)) {
        return res;
    }  
    return Arrays.asList(-1);
}

private boolean dfs(TreeNode root, int[] v) {
    if (root == null) {
        return true;
    }
    if (root.val != v[i++]) {
        return false;
    }
    if (root.left != null && root.left.val != v[i]) {
        res.add(root.val);
        return dfs(root.right, v) && dfs(root.left, v);
    } else {
        return dfs(root.left, v) && dfs(root.right, v);
    }
}
```



