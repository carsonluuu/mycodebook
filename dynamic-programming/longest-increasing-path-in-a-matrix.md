# Longest Increasing Path in a Matrix

Given an integer matrix, find the length of the longest increasing path.

From each cell, you can either move to four directions: left, right, up or down. You may NOT move diagonally or move outside of the boundary \(i.e. wrap-around is not allowed\).

### Example

**Example 1:**

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

**Example 2:**

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

Given a matrix:

\[  
\[1 ,2 ,3 ,4 ,5\],  
\[16,17,24,23,6\],  
\[15,18,25,22,7\],  
\[14,19,20,21,8\],  
\[13,12,11,10,9\]  
\]  
return 25

类似与滑雪问题  
这道题很容易想到二维dp， 记录f\[i\]\[j\] 是以i，j为结尾的LIS。但是由于我们走的方向不仅仅是从左往右和从上往下， 还可能从右往左和从下往上， 所以

```
1. 转化方程式非顺序性的(顺序指的是从左往右,从上往下)
2. 初始化的状态在哪儿是确定的
```

这样的问题, 我们只能dfs加记忆化搜索.  
每个位置最长的LIS记录在一个矩阵dp\[\]\[\] 里面, 同时用一个flag\[\]\[\] 矩阵记录下遍历过没有. dp和flag矩阵可以写在一起, 但是最好不要, 因为dp代表当前最长长度, flag代表遍历过没有, 意义不同.  
这道题的时间复杂度是O\(n\*n\), 因为有flag, 每个点最多遍历一次.

\(其实不需要flag，每个点其实也只是访问一次因为找路径\)

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



