# [Shortest Bridge](https://leetcode.com/problems/shortest-bridge/description/)

In a given 2D binary array`A`, there are two islands.  \(An island is a 4-directionally connected group of `1`s not connected to any other 1s.\)

Now, we may change`0`s to`1`s so as to connect the two islands together to form 1 island.

Return the smallest number of`0`s that must be flipped.  \(It is guaranteed that the answer is at least 1.\)

### Example

**Example 1:**

```
Input: [[0,1],[1,0]]
Output: 1
```

**Example 2:**

```
Input: [[0,1,0],[0,0,0],[0,0,1]]
Output: 2
```

**Example 3:**

```
Input: [[1,1,1,1,1],[1,0,0,0,1],[1,0,1,0,1],[1,0,0,0,1],[1,1,1,1,1]]
Output: 1
```

### Note

好题目，本质是求2个联通块之间的最短距离

方法就是去用dfs标记出一个岛，做一个以这个岛作为起点开始的多起点bfs，最边缘或者离另一个岛最近的点会最早扩张到另一个岛，输出层数即为距离

代码中利用一个found来做是否做完dfs的标示，然后岛1加入队列，向岛2扩张，找到2就结束输出level，是0就加入队列下一层去找，需要跳过是1的情况，是为了可以保证寻找到边缘的点

### Code

```java
class Solution {
    final int[][] DIR = new int[][]{{1, 0}, {-1, 0}, {0, 1}, {0, -1}};

    public int shortestBridge(int[][] matrix) {
        boolean found = false;
        Queue<int[]> q = new LinkedList<>();
        for (int i = 0; i < matrix.length; i++) {
            for (int j = 0; j < matrix[0].length; j++) {
                if (matrix[i][j] == 1 && !found) {
                    dfs(i, j, matrix);
                    found = true;
                }
                if (matrix[i][j] == 1 && found) {
                    q.offer(new int[]{i, j});
                }
            }
        }

        int level = 0;
        while (!q.isEmpty()) {
            int size = q.size();
            while (size-- > 0) {
                int[] curr = q.poll();
                for (int[] dir : DIR) {
                    int x = curr[0] + dir[0];
                    int y = curr[1] + dir[1];
                    if (!isValid(x, y, matrix)) {
                        continue;
                    }
                    if (matrix[x][y] == 2) {
                        return level;
                    } else if (matrix[x][y] == 1) {
                        continue;
                    } else if (matrix[x][y] == 0) {
                        matrix[x][y] = 1;
                        q.offer(new int[]{x, y});
                    }
                }
            }

            level++;
        }

        throw new IllegalArgumentException();
    }

    private void dfs(int x, int y, int[][] matrix) {
        if (!isValid(x, y, matrix)) {
            return;
        }
        if (matrix[x][y] != 1) {
            return;
        }

        matrix[x][y] = 2;
        for (int[] dir : DIR) {
            dfs(x + dir[0], y + dir[1], matrix);
        }
    }

    private boolean isValid(int x, int y, int[][] matrix) {
        return 0 <= x && x < matrix.length && 0 <= y && y < matrix[0].length;
    }
}
```



