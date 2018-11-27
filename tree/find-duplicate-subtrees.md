# Find Duplicate Subtrees

Given a binary tree, return all duplicate subtrees. For each kind of duplicate subtrees, you only need to return the root node of any **one **of them.

Two trees are duplicate if they have the same structure with same node values.

### Example

```
        1
       / \
      2   3
     /   / \
    4   2   4
       /
      4
```

The following are two duplicate subtrees:

```
      2
     /
    4
```

and

```
    4
```

Therefore, you need to return above trees' root in the form of a list.

### Note

Time: O\(N^2\)

Space: O\(N^2\)

### Code

```java
class Solution {
    public List<TreeNode> findDuplicateSubtrees(TreeNode root) {
        List<TreeNode> res = new ArrayList<>();
        Map<String, Integer> map = new HashMap<>();

        dfs(root, res, map);

        return res;
    }

    private String dfs(TreeNode root, List<TreeNode> res, 
                     Map<String, Integer> map) {
        if (root == null) return "#";
        String s = root.val + "," + dfs(root.left, res, map) + 
                              "," + dfs(root.right, res, map);
        map.put(s, map.getOrDefault(s, 0) + 1);
        if (map.get(s) == 2) {
            res.add(root);
        }

        return s;
    }
}
```



