# [01 Matrix](https://leetcode.com/problems/01-matrix/description/)

Given a matrix consists of 0 and 1, find the distance of the nearest 0 for each cell.

The distance between two adjacent cells is 1.

### Example

**Example 1:**  
Input:

```
0 0 0
0 1 0
0 0 0
```

Output:

```
0 0 0
0 1 0
0 0 0
```

**Example 2:**  
Input:

```
0 0 0
0 1 0
1 1 1
```

Output:

```
0 0 0
0 1 0
1 2 1
```

### Note

另一种距离的写法，有点DP的思想。

多起点队列，剩余的值写为MAX

```
matrix[nextX][nextY] <= matrix[x][y] + 1 ==> matrix[nextX][nextY] = matrix[x][y] + 1
```

Time O（n^2）Space O\(1\)

### Code

```java
class Solution {
    private static final int[][] DIR = new int[][]{{1, 0}, {-1, 0}, {0, 1}, {0, -1}};
    public int[][] updateMatrix(int[][] matrix) {
        int m = matrix.length, n = matrix[0].length;

        Queue<int[]> q = new LinkedList<>();
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (matrix[i][j] == 0) {
                    q.offer(new int[]{i, j});
                } else {
                    matrix[i][j] = Integer.MAX_VALUE;
                }
            }
        }

        while (!q.isEmpty()) {
            int[] curr = q.poll();
            int x = curr[0], y = curr[1];
            for (int[] dir : DIR) {
                int nextX = x + dir[0];
                int nextY = y + dir[1];
                if (nextX < 0 || nextX >= m || nextY < 0 || nextY >= n || 
                    matrix[nextX][nextY] <= matrix[x][y] + 1) continue;
                q.offer(new int[]{nextX, nextY});
                matrix[nextX][nextY] = matrix[x][y] + 1;
            }
        }
        return matrix;
    }
    /*
    [[0,0,0],
     [0,1,0],
     [1,1,1]]
    */
}
```



