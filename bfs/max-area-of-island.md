# [Max Area of Island](https://leetcode.com/problems/max-area-of-island/description/)

Given a non-empty 2D array`grid`of 0's and 1's, an**island**is a group of`1`'s \(representing land\) connected 4-directionally \(horizontal or vertical.\) You may assume all four edges of the grid are surrounded by water.

Find the maximum area of an island in the given 2D array. \(If there is no island, the maximum area is 0.\)

**Example 1:**

```
[[0,0,1,0,0,0,0,1,0,0,0,0,0],
 [0,0,0,0,0,0,0,1,1,1,0,0,0],
 [0,1,1,0,1,0,0,0,0,0,0,0,0],
 [0,1,0,0,1,1,0,0,1,0,1,0,0],
 [0,1,0,0,1,1,0,0,1,1,1,0,0],
 [0,0,0,0,0,0,0,0,0,0,1,0,0],
 [0,0,0,0,0,0,0,1,1,1,0,0,0],
 [0,0,0,0,0,0,0,1,1,0,0,0,0]]
```

Given the above grid, return`6`

. Note the answer is not 11, because the island must be connected 4-directionally.

**Example 2:**

```
[[0,0,0,0,0,0,0,0]]
```

Given the above grid, return`0`.

**Note:**The length of each dimension in the given`grid`does not exceed 50.

### Note

### Code

```java
class Solution {
    public int maxAreaOfIsland(int[][] grid) {
        int m = grid.length;
        int n = grid[0].length;
        int res = 0;
        int[][] d = new int[][]{{1,0},{-1,0},{0,1},{0,-1}};
        Queue<Integer> q = new LinkedList<>();
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == 1) {
                    int area = 0;
                    q.offer(n * i + j);
                    grid[i][j] = 0;
                    while (!q.isEmpty()) {
                        int cur = q.poll();
                        area++;
                        System.out.println(area);
                        int x = cur/n;
                        int y = cur%n;
                        for (int k = 0; k < 4; k++) {
                            int next_x = x + d[k][0];
                            int next_y = y + d[k][1];
                            if (next_x < m && next_x >= 0 
                                && next_y < n && next_y >= 0 
                                && grid[next_x][next_y] == 1) {
                                q.offer(n * next_x + next_y);
                                grid[next_x][next_y] = 0;
                            }
                        }
                    }
                res = Math.max(res, area);
                }
            }
        }
        return res;
    }
}

/*
    public int maxAreaOfIsland(int[][] grid) {
        int max_area = 0;
        for(int i = 0; i < grid.length; i++)
            for(int j = 0; j < grid[0].length; j++)
                if(grid[i][j] == 1)max_area = Math.max(max_area, AreaOfIsland(grid, i, j));
        return max_area;
    }
    
    public int AreaOfIsland(int[][] grid, int i, int j){
        if( i >= 0 && i < grid.length && j >= 0 && j < grid[0].length && grid[i][j] == 1){
            grid[i][j] = 0;
            return  1 + AreaOfIsland(grid, i+1, j) + 
                        AreaOfIsland(grid, i-1, j) + 
                        AreaOfIsland(grid, i, j-1) + 
                        AreaOfIsland(grid, i, j+1);
        }
        return 0;
    }
*/
```



