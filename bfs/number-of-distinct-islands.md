# [Number of Distinct Islands](https://leetcode.com/problems/number-of-distinct-islands/description/)

Given a non-empty 2D array`grid`of 0's and 1's, an **island **is a group of`1`'s \(representing land\) connected 4-directionally \(horizontal or vertical.\) You may assume all four edges of the grid are surrounded by water.

Count the number of **distinct **islands. An island is considered to be the same as another if and only if one island can be translated \(and not rotated or reflected\) to equal the other.

### Example

**Example 1:**

```
11000
11000
00011
00011
```

Given the above grid map, return`1`.

**Example 2:**

```
11011
10000
00001
11011
```

Given the above grid map, return`3`.

Notice that:

```
11
1
```

and

```
 1
11
```

are considered different island shapes, because we do not consider reflection / rotation.

### Note

利用BFS暴力去做, 找到岛屿单元的相对坐标， 使用hashset， set 里面是BFS返回的一系列坐标

### Code

```java
class Solution {
    
    final int[] dx = {0, 0, 1, -1};
    final int[] dy = {1, -1, 0, 0};
    public int numDistinctIslands(int[][] grid) {
        if (grid == null || grid.length == 0 || grid[0].length == 0){
            return 0;
        }
        
        Set<List<List<Integer>>> set = new HashSet<>();
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j <grid[0].length; j++) {
                if (grid[i][j] == 1) {
                    List<List<Integer>> list = bfs(grid, i, j);
                    set.add(list);
                }
            }
        }
        return set.size();
    }
    
    private List<List<Integer>> bfs(int[][] grid, int a, int b) {
        List<List<Integer>> res = new ArrayList<>();
        int m = grid.length, n = grid[0].length;
        Queue<Integer> qx = new LinkedList<>();
        Queue<Integer> qy = new LinkedList<>();
        qx.offer(a);
        qy.offer(b);
        while (!qx.isEmpty() && !qy.isEmpty()) {
            int x = qx.poll();
            int y = qy.poll();
            List<Integer> list = new ArrayList<>();
            list.add(x - a);
            list.add(y - b);
            res.add(list);
            for (int i = 0; i < 4; i++) {
                int nx = x +dx[i];
                int ny = y + dy[i];
                if(nx >= 0 &&nx < m && ny >= 0 && ny < n && grid[nx][ny] == 1){
                    grid[nx][ny] = 0;
                    qx.offer(nx);
                    qy.offer(ny);
                }
            }
        }
        return res;
    }
}
```



