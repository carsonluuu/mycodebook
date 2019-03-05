# [Unique Paths III](https://leetcode.com/problems/unique-paths-iii/description/)

On a 2-dimensional `grid`, there are 4 types of squares:

* `1`represents the starting square.  There is exactly one starting square.
* `2`represents the ending square.  There is exactly one ending square.
* `0`represents empty squares we can walk over.
* `-1`represents obstacles that we cannot walk over.

Return the number of 4-directional walks from the starting square to the ending square, that**walk over every non-obstacle square exactly once**.

### Example

**Example 1:**

```
Input: 
[[1,0,0,0],[0,0,0,0],[0,0,2,-1]]
Output: 
2
Explanation: 
We have the following two paths: 
1. (0,0),(0,1),(0,2),(0,3),(1,3),(1,2),(1,1),(1,0),(2,0),(2,1),(2,2)
2. (0,0),(1,0),(2,0),(2,1),(1,1),(0,1),(0,2),(0,3),(1,3),(1,2),(2,2)
```

**Example 2:**

```
Input: 
[[1,0,0,0],[0,0,0,0],[0,0,0,2]]
Output: 
4
Explanation: 
We have the following four paths: 
1. (0,0),(0,1),(0,2),(0,3),(1,3),(1,2),(1,1),(1,0),(2,0),(2,1),(2,2),(2,3)
2. (0,0),(0,1),(1,1),(1,0),(2,0),(2,1),(2,2),(1,2),(0,2),(0,3),(1,3),(2,3)
3. (0,0),(1,0),(2,0),(2,1),(2,2),(1,2),(1,1),(0,1),(0,2),(0,3),(1,3),(2,3)
4. (0,0),(1,0),(2,0),(2,1),(1,1),(0,1),(0,2),(0,3),(1,3),(1,2),(2,2),(2,3)
```

**Example 3:**

```
Input: 
[[0,1],[2,0]]
Output: 
0
Explanation: 

There is no path that walks over every empty square exactly once.
Note that the starting and ending square can be anywhere in the grid.

```

### Note

Time\(4^mn\)

Space\(m\*n\)

暴力backtracking去搜索，直到到达终点的时候，路径点都被访问

返回值是路径数目

### Code

```java
class Solution {
    public int uniquePathsIII(int[][] grid) {
        int sx = -1, sy = -1;
        int count = 0; 
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                if (grid[i][j] == 0) {
                    count++;
                } else if (grid[i][j] == 1) {
                    sx = i; sy = j;
                    count++;
                }
            }
        }
        
        return dfs(grid, sx, sy, count);
    }
    
    private int dfs(int[][] grid, int x, int y, int count) {
        if (!check(grid, x, y)) {
            return 0;
        }
        if (grid[x][y] == 2) {
            return count == 0 ? 1 : 0;
        }
        
        grid[x][y] = -1;
        int res = dfs(grid, x, y - 1, count - 1) + 
                  dfs(grid, x, y + 1, count - 1) + 
                  dfs(grid, x - 1, y, count - 1) + 
                  dfs(grid, x + 1, y, count - 1);
        grid[x][y] = 0;
        return res;
    }
    
    public boolean check(int[][] grid, int i, int j) {
        int m = grid.length, n = grid[0].length;
        return 0 <= i && i < m && 0 <= j && j < n && grid[i][j] != -1;
    }
}
```



