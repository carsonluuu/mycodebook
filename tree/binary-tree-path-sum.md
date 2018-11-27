# Path Sum III

Your are given a binary tree in which each node contains a value. Design an algorithm to get all paths which sum to a given value. The path does not need to start or end at the root or a leaf, but it must go in a straight line down.

### Example

Given a binary tree:

```
    1
   / \
  2   3
 /   /
4   2
```

for target =`6`, return

```
[
  [2, 4],
  [1, 3, 2]
]
```

### Note

在2的基础上要求输出所有路径了

分为三个问题:

1. path在左
2. path在右
3. path以root开始

难的是一定以1开始, 和为6, 又是一个分治, 分为: 一定以2出发和一定以3出发的

O\(n^2\)

从路径列表最后开始遍历，和为目标值则deep copy一个加入结果

```java
public class Solution {
    /*
     * @param root: the root of binary tree
     * @param target: An integer
     * @return: all valid paths
     */
    public List<List<Integer>> binaryTreePathSum(TreeNode root, 
                                                  int target) {
        List<List<Integer>> result = new ArrayList<>();
        if (root != null) {
            helper(root, target, new ArrayList<Integer>(), result);
        }
        return result;
    }

    private void helper(TreeNode root, int target, List<Integer> path, List<List<Integer>> result) {
        if (root == null) {
            return;
        }
        path.add(root.val);
        int sum = 0;
        for (int i = path.size() - 1; i >= 0; i--) {
            sum += path.get(i);
            if (sum == target) {
                result.add(new ArrayList<Integer>(path.subList(i, path.size())));
            }
        }
        helper(root.left, target, path, result);
        helper(root.right, target, path, result);
        path.remove(path.size() - 1);
    }
}
```



