# Binary Tree Maximum Path Sum

Given a **non-empty **binary tree, find the maximum path sum.

For this problem, a path is defined as any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The path must contain **at least one node **and does not need to go through the root.

### Example

**Example 1:**

```
Input: [1,2,3]

       1
      / \
     2   3

Output: 6
```

**Example 2:**

```
Input: [-10,9,20,null,null,15,7]

   -10
   / \
  9  20
    /  \
   15   7

Output: 42
```

### Note

使用ResultType：

```
singlePath: 从root往下走到任意点的最大路径，这条路径可以不包含任何点
maxPath: 从树中任意到任意点的最大路径，这条路径至少包含一个点
如果节点为空：singlePath = 0，maxPath = -inf
```

```
singlePath = root值加上左右singlePath的更大者 并维护singlePath >= 0 
maxPath = 左右maxPath的更大者， 维护maxPath为root值加上左右singlePath
```

直接比较：

定义全局变量res，并求左右子树的最大值

结果为`max(res, root.val, left + root.val + right, left + root.val, right + root.val)`

分治left和right，对于helper函数，返回值是`max(root.val, root.val + left, root.val + right)`，维护结果值res:

* left为负数：最大值是`max(res, root.val, root.val + right)`
* right为负数：最大值是`max(res, root.val, root.val + left)`
* 都不为负：最大值是`max(res, root.val + left + right)`

最大和路径有这么几种可能：

* 从 root 出发，路上看到负数，不采用；
* 从 root 出发，路上看到负数，负数后面存在总和超过负数节点的路径；
* 最大和在某个从 leaf node 往上走的一条路径上，不过 root.
* 左路径最大，采用左路径；
* 右路径最大，采用右路径；
* 单独节点最大，可能是 左/右/根 其中之一。

换句话说，一个重要的问题是，我们只能从 root 开始，也没有 parent 指针，但是最优的路径可能却和 root 是不连续的，这就切断了 Binary Tree divide & conquer / Tree DFS 里面大多数做法中非常依赖的性质，即层层递归之前 左/右 子树和根节点的联系。

### Code

```java
public class Solution {
        private class ResultType {
            int singlePath, maxPath; 
            ResultType(int singlePath, int maxPath) {
                this.singlePath = singlePath;
                this.maxPath = maxPath;
            }
        }

        private ResultType helper(TreeNode root) {
            if (root == null) {
                return new ResultType(0, Integer.MIN_VALUE);
            }
            // Divide
            ResultType left = helper(root.left);
            ResultType right = helper(root.right);

            // Conquer
            int singlePath = Math.max(left.singlePath, right.singlePath) + root.val;
            singlePath = Math.max(singlePath, 0);

            int maxPath = Math.max(left.maxPath, right.maxPath);
            maxPath = Math.max(maxPath, left.singlePath + right.singlePath + root.val);

            return new ResultType(singlePath, maxPath);
        }

        public int maxPathSum(TreeNode root) {
            ResultType result = helper(root);
            return result.maxPath;
        }
}
```

```java
class Solution {
    int res = Integer.MIN_VALUE;

    public int maxPathSum(TreeNode root) {
        if (root == null) {
            return 0;
        }

        int left  = helper(root.left);
        int right = helper(root.right);

        return max(res, root.val, 
                    left + root.val + right, 
                    left + root.val,
                    right + root.val);
    }

    private int helper(TreeNode root) {
        if (root == null) {
            return 0;
        }

        int left  = helper(root.left);
        int right = helper(root.right);
        if (left < 0) {
            res = max(res, root.val, root.val + right);
        } else if (right < 0) {
            res = max(res, root.val, root.val + left);
        } else {
            res = Math.max(res, root.val + left + right);
        }

        return max(root.val, root.val + left, root.val + right);
    }

    private int max(int a, int b, int c) {
        return Math.max(a, Math.max(b, c));
    }

    private int max(int a, int b, int c, int d, int e) {
        return max(max(a, b, c), d, e);
    }
}
```



