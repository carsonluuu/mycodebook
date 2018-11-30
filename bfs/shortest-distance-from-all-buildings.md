# [Shortest Distance from All Buildings](https://leetcode.com/problems/shortest-distance-from-all-buildings/description/)

You want to build a house on anemptyland which reaches all buildings in the shortest amount of distance. You can only move up, down, left and right. You are given a 2D grid of values **0**,**1 **or **2**, where:

* Each **0 **marks an empty land which you can pass by freely.
* Each **1 **marks a building which you cannot pass through.
* Each **2 **marks an obstacle which you cannot pass through.

**Note:**

There will be at least one building. If it is not possible to build such house according to the above rules, return -1.

### Example

```
Input: [[1,0,2,0,1],[0,0,0,0,0],[0,0,1,0,0]]

1 - 0 - 2 - 0 - 1
|   |   |   |   |
0 - 0 - 0 - 0 - 0
|   |   |   |   |
0 - 0 - 1 - 0 - 0

Output: 7 

Explanation: Given three buildings at (0,0), (0,4), (2,2), and an obstacle at (0,2),
             the point (1,2) is an ideal empty land to build a house, as the total 
             travel distance of 3+3+1=7 is minimal. So return 7.
```

### Note

O\(m^2\*n^2\)的BFS做法

对于每个空地做一下BFS，然后算到各个建筑最近距离和；然后找出最小的那个空地

### Code

```java
class Solution {
    private static class Point {
        public int x;
        public int y;

        public Point(int x, int y) {
            this.x = x;
            this.y = y;
        }
    }
    private final int[] dx = {1, 0, -1, 0}, dy = {0, 1, 0, -1};

    public int shortestDistance(int[][] grid) {
        int m = grid.length, n = grid[0].length;
        int[][] dist = new int[m][n];
        int[][] reach = new int[m][n];

        int count = 0;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == 1) {
                    count++;
                    bfs(new Point(i, j), grid, dist, reach);
                }
            }
        }

        int shortest = Integer.MAX_VALUE;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == 0 && reach[i][j] == count) {
                    shortest = Math.min(shortest, dist[i][j]);
                }
            }
        }
        return shortest == Integer.MAX_VALUE ? -1 : shortest;
    }

    private void bfs(Point p, int[][] grid, 
                     int[][] dist, int[][] reach) {
        int m = grid.length, n = grid[0].length;
        Queue<Point> q = new LinkedList<>();
        boolean[][] visited = new boolean[m][n];

        q.offer(p);
        int level = 1;
        while (!q.isEmpty()) {
            int size = q.size();
            while (size-- > 0) {
                Point curr = q.poll();
                for (int dir = 0; dir < 4; dir++) {
                    int x = curr.x + dx[dir];
                    int y = curr.y + dy[dir];
                    Point next = new Point(x, y);
                    if (x < 0 || x >= m || 
                        y < 0 || y >= n || grid[x][y] != 0 ) {
                        continue;
                    }
                    if (!visited[x][y]) {
                        dist[x][y] += level;
                        reach[x][y]++;
                        q.offer(next);
                        visited[x][y] = true;
                    }
                }
            }
            level++;
        } 
    }
}
```



