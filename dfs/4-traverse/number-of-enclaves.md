# [Number of Enclaves](https://leetcode.com/problems/number-of-enclaves/description/)

Given a 2D array`A`, each cell is 0 \(representing sea\) or 1 \(representing land\)

A move consists of walking from one land square 4-directionally to another land square, or off the boundary of the grid.

Return the number of land squares in the grid for which we**cannot**walk off the boundary of the grid in any number of moves.

### Example

**Example 1:**

```
Input: 
[[0,0,0,0],[1,0,1,0],[0,1,1,0],[0,0,0,0]]
Output: 
3
Explanation: 

There are three 1s that are enclosed by 0s, and one 1 that isn't enclosed because its on the boundary.
```

**Example 2:**

```
Input: 
[[0,1,1,0],[0,0,1,0],[0,0,1,0],[0,0,0,0]]
Output: 
0
Explanation: 

All 1s are either on the boundary or can reach the boundary.
```

### Note

边界起点的DFS遍历，把和边界相连的1都变成0，然后剩余的count就是记录结果的1的数目

### Code

```java
class Solution {
    /*
    [[0,0,0,0],
     [1,0,1,0],
     [0,1,1,0],
     [0,0,0,0]]
    */
    public int numEnclaves(int[][] A) {
        
        for (int i = 0; i < A.length; i++) {
            for (int j = 0; j < A[0].length; j++) {
                if (i == 0 || i == A.length - 1 ||
                    j == 0 || j == A[0].length - 1) {
                    dfs(A, i, j);
                }
            }
        }
        
        int res = 0;
        for (int i = 0; i < A.length; i++) {
            for (int j = 0; j < A[0].length; j++) {
                if (A[i][j] == 1) {
                    res++;
                }
            }
        }
        
        return res;
    }
    
    private void dfs(int[][] A, int i, int j) {
        if (i < 0 || i >= A.length || 
            j < 0 || j >= A[0].length ||
            A[i][j] == 0) {
            return;
        }
        A[i][j] = 0;
        dfs(A, i - 1, j);
        dfs(A, i + 1, j);
        dfs(A, i, j - 1);
        dfs(A, i, j + 1);
    }
}
```



