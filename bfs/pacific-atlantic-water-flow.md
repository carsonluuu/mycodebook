# [Pacific Atlantic Water Flow](https://leetcode.com/problems/pacific-atlantic-water-flow/description/)

Given an`m x n`matrix of non-negative integers representing the height of each unit cell in a continent, the "Pacific ocean" touches the left and top edges of the matrix and the "Atlantic ocean" touches the right and bottom edges.

Water can only flow in four directions \(up, down, left, or right\) from a cell to another one with height equal or lower.

Find the list of grid coordinates where water can flow to both the Pacific and Atlantic ocean.

**Note**

1. The order of returned grid coordinates does not matter.
2. Both m and n are less than 150.

### **Example**

```
Given the following 5x5 matrix:

  Pacific ~   ~   ~   ~   ~ 
       ~  1   2   2   3  (5) *
       ~  3   2   3  (4) (4) *
       ~  2   4  (5)  3   1  *
       ~ (6) (7)  1   4   5  *
       ~ (5)  1   1   2   4  *
          *   *   *   *   * Atlantic

Return:

[[0, 4], [1, 3], [1, 4], [2, 2], [3, 0], [3, 1], [4, 0]] (positions with parentheses in above matrix).
```

### Note

也是属于外层到内层的遍历，反向流，找递增的路径，太平洋和大西洋分别走一个BFS，并mark with BFS 求两个visited数组的交集

### Code

```java
class Solution {
    class Node {
        int x, y;
        Node (int x, int y) {
            this.x = x;
            this.y = y;
        }
    }

    final int[][] dir = new int[][]{{1, 0}, {-1, 0}, {0, 1}, {0, -1}};
    int m, n;

    public List<int[]> pacificAtlantic(int[][] matrix) {
        List<int[]> res = new ArrayList<>();
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return res;
        }

        m = matrix.length;
        n = matrix[0].length;
        boolean[][] visitedP = new boolean[m][n];
        boolean[][] visitedA = new boolean[m][n];
        Queue<Node> pQueue = new LinkedList<>();
        Queue<Node> aQueue = new LinkedList<>();

        for (int i = 0; i < m; i++) {
            visitedP[i][0] = true;
            pQueue.offer(new Node(i, 0));
            visitedA[i][n - 1] = true;
            aQueue.offer(new Node(i, n - 1));
        }
        for (int j = 0; j < n; j++) {
            visitedP[0][j] = true;
            pQueue.offer(new Node(0, j));
            visitedA[m - 1][j] = true;
            aQueue.offer(new Node(m - 1, j));
        }

        bfs(matrix, pQueue, visitedP);
        bfs(matrix, aQueue, visitedA);

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (visitedP[i][j] && visitedA[i][j]) {
                    res.add(new int[]{i, j});
                }
            }
        }

        return res;
    }

    private void bfs(int[][] matrix, Queue<Node> q, boolean[][] visited) {
        while (!q.isEmpty()) {
            Node curr = q.poll();
            for (int i = 0; i < 4; i++) {
                int x = curr.x + dir[i][0];
                int y = curr.y + dir[i][1];
                if (inBoundary(x, y, matrix) && 
                    !visited[x][y] &&
                    matrix[x][y] >= matrix[curr.x][curr.y]) {
                    q.offer(new Node(x, y));
                    visited[x][y] = true;
                }
            }
        }
    }

    private boolean inBoundary(int x, int y, int[][] matrix) {
        return (x >= 0 && y >= 0 &&
                x < m && y < n);
    }
}
```



