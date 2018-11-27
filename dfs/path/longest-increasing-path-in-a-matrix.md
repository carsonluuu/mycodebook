# Longest Increasing Path in a Matrix

Given an integer matrix, find the length of the longest increasing path.

From each cell, you can either move to four directions: left, right, up or down. You may NOT move diagonally or move outside of the boundary \(i.e. wrap-around is not allowed\).

### Example

**Example 1**

```
Input: nums = 
[
  [9,9,4],
  [6,6,8],
  [2,1,1]
] 
Output: 4 
Explanation: The longest increasing path is [1, 2, 6, 9].
```

**Example 2**

```
Input: nums = 
[
  [3,4,5],
  [3,2,6],
  [2,2,1]
] 
Output: 4 
Explanation: The longest increasing path is [3, 4, 5, 6]. Moving diagonally is not allowed.
```

### Note

memo -&gt; result for Node\(i, j\)

each Node we apply the dfs search

Time complexity :O\(mn\). Each vertex/cell will be calculated once and only once, and each edge will be visited once and only once. The total time complexity is thenO\(V+E\).VVis the total number of vertices andEEis the total number of edges. In our problem,O\(V\)=O\(mn\),O\(E\) = O\(4V\) = O\(mn\).

Space complexity :O\(mn\). The cache dominates the space complexity.

### Code

```java
class Solution {
    public int longestIncreasingPath(int[][] matrix) {
        if (matrix == null || matrix.length == 0 ||
            matrix[0] == null || matrix[0].length == 0) {
            return 0;
        }

        int res = 0, m = matrix.length, n = matrix[0].length;
        int[][] memo = new int[m][n]; //res from Node (i,j)

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                res = Math.max(res, dfs(matrix, i, j, memo));
            }
        }

        return res;
    }

    private int dfs(int[][] matrix, int i, int j, int[][] memo) {
        if (memo[i][j] != 0) {
            return memo[i][j];
        }

        int m = matrix.length, n = matrix[0].length;
        int[][] dir = new int[][]{{1, 0},{0, 1},{-1, 0},{0, -1}};
        for (int k = 0; k < dir.length; k++) {
            int x = dir[k][0] + i;
            int y = dir[k][1] + j;
            if (x >= 0 && x < m && y >= 0 && y < n &&
                matrix[x][y] > matrix[i][j]) {
                memo[i][j] = Math.max(memo[i][j], dfs(matrix, x, y, memo));
            }
        }
        memo[i][j] += 1;

        return memo[i][j];
    }
}
```



