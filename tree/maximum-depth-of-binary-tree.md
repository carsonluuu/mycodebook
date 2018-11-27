# Max/Min Depth of Binary Tree

For a tree, depth equals to height.

**Max**

Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

**Note:** A leaf is a node with no children.

**Example:**

Given binary tree`[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

return its depth = 3.

```java
//Divide and Conquer
class Solution {
    public int maxDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }

        int left = maxDepth(root.left);
        int right = maxDepth(root.right);

        return Math.max(left, right) + 1;
    }
}
```

```java
//*Traverse
Class Solution {
    private int depth;
    public int maxDepth(TreeNode root) {
        depth = 0;

        helper(root, 1);

        return depth;
    }

    private void helper(TreeNode root, int currDepth) {
        if (node == null) {
            return;
        }

        depth = Math.max(depth, currDepth);

        helper(root.left,  currDepth + 1);
        helper(root.right, currDepth + 1);
    }
}
```

```java
//Iteration - Do the level order
public class Solution {
    public int maxDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        int depth = 0;
        while (!queue.isEmpty()) {
            int size = queue.size();
            depth++;
            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();
                if (node.left != null) {
                    queue.offer(node.left);    
                }

                if (node.right != null) {
                    queue.offer(node.right);
                }
            }
        }

        return depth;
    }
}
```

**Min**

Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

**Note:** A leaf is a node with no children.

**Example:**

Given binary tree`[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

return its minimum depth = 2.

```java
//Divide and conquer.
class Solution {
    public int minDepth(TreeNode root) {
        if (root == null) {
            return 0;
        // leaf node
        if (root.left == null && root.right == null) {
            return 1;
        }
        // left or right child is empty than go for the other side for ans
        if (root.left == null) {
            return minDepth(root.right) + 1;
        }
        if (root.right == null) {
            return minDepth(root.left) + 1;
        }

        return Math.min(minDepth(root.left), minDepth(root.right)) + 1;
    }
}
```

```java
//Traverse
public class Solution {
    private int depth = Integer.MAX_VALUE;

    public int minDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }

        helper(root, 1);

        return depth;
    }

    public void helper(TreeNode root, int curdepth) {
        if (root == null) {
            return;
        }
        //to leaf node
        if (root.left == null && root.right == null && curdepth < depth) {  
            depth = curdepth;
        }

        helper(root.left, curdepth + 1);
        helper(root.right, curdepth + 1);
    } 
}
```

```java
//Iteration - go for first leaf node
public class Solution {
    public int minDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        int depth = 0;
        while (!queue.isEmpty()) {
            int size = queue.size();
            depth++;
            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();
                if (node.left == null && node.right == null) {
                    return depth;     
                }

                if (node.left != null) {
                    queue.offer(node.left);    
                }

                if (node.right != null) {
                    queue.offer(node.right);
                }
            }
        }

        return 0;
    }
}
```



