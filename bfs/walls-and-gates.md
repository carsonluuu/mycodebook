# [Walls and Gates](https://leetcode.com/problems/walls-and-gates/description/)

You are given am 2D grid initialized with these three possible values.

```
1. -1 - A wall or an obstacle.
2. 0 - A gate.
3. INF - Infinity means an empty room. （2147483647）.
```

Fill each empty room with the distance to its nearest gate. If it is impossible to reach a gate, it should be filled with`INF`.

### **Example**

Given the 2D grid:

```
INF  -1  0  INF
INF INF INF  -1
INF  -1 INF  -1
  0  -1 INF INF
```

After running your function, the 2D grid should be:

```
  3  -1   0   1
  2   2   1  -1
  1  -1   2  -1
  0  -1   3   4
```

### Note

多起点的BFS求最短距离，这里把门作为起点加入队列

必须满足：

```
cur.value + 1 < rooms[next_x][next_y]
```

因为我们求最短距离

### Code

```java
class Solution {
    public void wallsAndGates(int[][] rooms) {
        class Node {
            public int x, y, value;
            public Node(int x, int y, int value) {
                this.x = x;
                this.y = y;
                this.value = value;
            }
        }

        int INF = 2147483647;
        int n = rooms.length;
        if (n == 0) return;
        int m = rooms[0].length;
        Queue<Node> q = new LinkedList<>();
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (rooms[i][j] == 0) {
                    q.offer(new Node(i, j, rooms[i][j]));
                }
            }
        }
        int[][] d = new int[][]{{1,0},{-1,0},{0,1},{0,-1}};
        while (!q.isEmpty()) {
            Node cur = q.poll();
            for (int i = 0; i < 4; i++) {
                int next_x = cur.x + d[i][0];
                int next_y = cur.y + d[i][1];
                Node next = new Node(next_x, next_y, 0);
                if (next_x >= 0 && next_x < n && next_y >= 0 
                    && next_y < m && rooms[next_x][next_y] != -1
                    && cur.value + 1 < rooms[next_x][next_y]) {
                    next.value = cur.value + 1;
                    rooms[next_x][next_y] = next.value;
                    q.offer(next);
                }
            }
        }

    }
}
```



