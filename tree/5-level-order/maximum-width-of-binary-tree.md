# [Maximum Width of Binary Tree](https://leetcode.com/problems/maximum-width-of-binary-tree/description/)

Given a binary tree, write a function to get the maximum width of the given tree. The width of a tree is the maximum width among all levels. The binary tree has the same structure as a **full binary tree**, but some nodes are null.

The width of one level is defined as the length between the end-nodes \(the leftmost and right most non-null nodes in the level, where the`null`nodes between the end-nodes are also counted into the length calculation.

### Example

**Example 1:**

```
Input:
           1
         /   \
        3     2
       / \     \  
      5   3     9 

Output:
 4

Explanation:
 The maximum width existing in the third level with the length 4 (5,3,null,9).
```

**Example 2:**

```
Input:

          1
         /  
        3    
       / \       
      5   3     


Output:
 2

Explanation:
 The maximum width existing in the third level with the length 2 (5,3).
```

**Example 3:**

```
Input:
          1
         / \
        3   2 
       /        
      5      

Output:
 2

Explanation:
 The maximum width existing in the second level with the length 2 (3,2).
```

**Example 4:**

```
Input:

          1
         / \
        3   2
       /     \  
      5       9 
     /         \
    6           7

Output:
 8
Explanation:
The maximum width existing in the fourth level with the length 8 (6,null,null,null,null,null,null,7).
```

### Note

这题的核心：

1. 层次遍历的实现（递归/迭代）
2. 树孩子的index，最右边减去最左边：`left = 2 * index， right = 2 * index + 1`

### Code

**迭代**

```java
class Solution {
    public int widthOfBinaryTree(TreeNode root) {
        int res = 0;
        if (root == null) {
            return res;
        }

        Queue<TreeNode> q = new LinkedList<>();
        Map<TreeNode, Integer> map = new HashMap<>();
        q.offer(root);
        map.put(root, 1);
        while (!q.isEmpty()) {
            int size = q.size();
            int start = 0, end = 0;
            for (int i = 0; i < size; i++) {
                TreeNode curr = q.poll();
                if (i == 0) {
                    start = map.get(curr);
                }
                if (i == size - 1) {
                    end = map.get(curr);
                }
                if (curr.left != null) {
                    map.put(curr.left, map.get(curr) * 2);
                    q.offer(curr.left);
                } 
                if (curr.right != null) {
                    q.offer(curr.right);
                    map.put(curr.right, map.get(curr) * 2 + 1);
                }
            }
            res = Math.max(res, end - start + 1);
        }

        return res;
    }
}
```

**递归**

```java
public int widthOfBinaryTree(TreeNode root) {
    int res = 0;
    if (root == null) {
        return res;
    }

    return dfs(root, 0, 1, new ArrayList<>(), new ArrayList<>());
}

private int dfs(TreeNode root, int level, int index, 
                 List<Integer> start, List<Integer> end) {
    if (root == null) {
        return 0;
    }

    if (level == start.size()) {
        start.add(index);
        end.add(index);
    } else {
        end.set(level, index);
    }

    int curr = end.get(level) - start.get(level) + 1;
    int left = dfs(root.left, level + 1, index * 2, start, end);
    int right = dfs(root.right, level + 1, index * 2 + 1, start, end);

    return Math.max(curr, Math.max(left, right));
}
```



