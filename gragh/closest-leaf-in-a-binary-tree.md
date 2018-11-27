# Closest Leaf in a Binary Tree

Given a binary tree **where every node has a unique value**, and a target key`k`, find the value of the nearest leaf node to target`k`in the tree.

Here,nearestto a leaf means the least number of edges travelled on the binary tree to reach any leaf of the tree. Also, a node is called aleafif it has no children.

In the following examples, the input tree is represented in flattened form row by row. The actual`root`tree given will be a TreeNode object.

### Example

**Example 1:**

```
Input: root = [1, 3, 2], k = 1
Diagram of binary tree:
          1
         / \
        3   2

Output: 2 (or 3)

Explanation: Either 2 or 3 is the nearest leaf node to the target of 1.
```

**Example 2:**

```
Input: root = [1], k = 1

Output: 1

Explanation: The nearest leaf node is the root node itself.
```

**Example 3:**

```
Input: root = [1,2,3,4,null,null,null,5,null,6], k = 2
Diagram of binary tree:
             1
            / \
           2   3
          /
         4
        /
       5
      /
     6
Output: 3
Explanation: The leaf node with value 3 (and not the leaf node with value 6) is nearest to the node with value 2.
```

### Note

DFS寻找目标并构建，backward map作为parent node

BFS上下进行遍历，寻找下一层的叶子结点

### Code

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public int findClosestLeaf(TreeNode root, int k) {
        Map<TreeNode, TreeNode> backMap = new HashMap<>();

        TreeNode node = dfs(root, k, backMap);

        return bfs(node, backMap);
    }

    private int bfs(TreeNode node, Map<TreeNode, TreeNode> backMap) {
        Queue<TreeNode> q = new LinkedList<>();
        Set<TreeNode> set = new HashSet<>();
        q.offer(node);
        set.add(node);
        while (!q.isEmpty()) {
            int size = q.size();
            for (int i = 0; i < size; i++) {
                TreeNode curr = q.poll();
                if (curr.left == null && curr.right == null) {
                    return curr.val;
                }
                if (curr.left != null && !set.contains(curr.left)) {
                    q.offer(curr.left);
                    set.add(curr.left);
                }
                if (curr.right != null && !set.contains(curr.right)) {
                    q.offer(curr.right);
                    set.add(curr.right);
                }
                if (backMap.get(curr) != null && !set.contains(backMap.get(curr))) {
                    q.offer(backMap.get(curr));
                    set.add(backMap.get(curr));
                }
            }
        }

        return -1;
    }

    private TreeNode dfs(TreeNode root, int k, Map<TreeNode, TreeNode> backMap) {
        if (root.val == k) {
            return root;
        }
        if (root.left != null) {
            backMap.put(root.left, root);
            TreeNode left = dfs(root.left, k, backMap);
            if (left != null) {
                return left;
            }
        }
        if (root.right != null) {
            backMap.put(root.right, root);
            TreeNode right = dfs(root.right, k, backMap);
            if (right != null) {
                return right;
            }
        }

        return null;
    }
}
```



