# [Surrounded Regions](https://leetcode.com/problems/surrounded-regions/description/)

Given a 2D board containing`'X'`and`'O'`\(**the letter O**\), capture all regions surrounded by`'X'`.

A region is captured by flipping all`'O'`s into`'X'`s in that surrounded region.

### **Example**

```
X X X X
X O O X
X X O X
X O X X
```

After running your function, the board should be:

```
X X X X
X X X X
X X X X
X O X X
```

**Explanation:**

Surrounded regions shouldn’t be on the border, which means that any`'O'` on the border of the board are not flipped to`'X'`. Any`'O'` that is not on the border and it is not connected to an`'O'` on the border will be flipped to`'X'`. Two cells are connected if they are adjacent cells connected horizontally or vertically.

### Note

其实用Union-Find比较贴切

bfs/dfs 思路类似，得从周围一圈找“O”搞进去，和边缘相连的就不能被一起改了

改完然后再处理一遍

### Code

```java
class Solution {
    public void solve(char[][] board) {
        if (board == null || 0 == board.length || 0 == board[0].length) return;
        
        int m = board.length - 1;
        int n = board[0].length - 1;
        
        for (int i = 0; i <= m; i++) {
            if (board[i][0] == 'O')
                dfs(board, i, 0);
            if (board[i][n] == 'O')
                dfs(board, i, n);
        }
        for (int j = 0; j <= n; j++) {
            if (board[0][j] == 'O')
                dfs(board, 0, j);
            if (board[m][j] == 'O')
                dfs(board, m, j);
        }
        for (int i = 0; i <= m; i++)
            for (int j = 0; j <= n; j++) {
                if (board[i][j] == 'O')
                    board[i][j] = 'X';
                else if (board[i][j] == '1')
                    board[i][j] = 'O';
            }
    }
    
    private void dfs(char[][] board, int x, int y) {
        if ( x<0|| y<0 || x>=board.length || y >=board[0].length || board[x][y] != 'O' ) return;
        board[x][y] = '1';
        dfs(board, x - 1, y);
        dfs(board, x + 1, y);
        dfs(board, x, y - 1);
        dfs(board, x, y + 1);
    }
}
```

```java
public class Solution {
    static final int[] directionX = {+1, -1, 0, 0};
    static final int[] directionY = {0, 0, +1, -1};

    static final char FREE = 'F';
    static final char TRAVELED = 'T';

    public void solve(char[][] board) {
        if (board.length == 0) {
            return;
        }

        int row = board.length;
        int col = board[0].length;

        for (int i = 0; i < row; i++) {
            bfs(board, i, 0);
            bfs(board, i, col - 1);
        }

        for (int j = 1; j < col - 1; j++) {
            bfs(board, 0, j);
            bfs(board, row - 1, j);
        }

        for (int i = 0; i < row; i++) {
            for (int j = 0; j < col; j++) {
                switch(board[i][j]) {
                    case 'O': 
                        board[i][j] = 'X';
                        break;
                    case 'F':
                        board[i][j] = 'O';
                }
            }
        }
    }

    public void bfs(char[][] board, int i, int j) {
        if (board[i][j] != 'O') {
            return;
        }

        Queue<Node> queue = new LinkedList<Node>();
        queue.offer(new Node(i, j));

        while (!queue.isEmpty()) {
            Node crt = queue.poll();
            board[crt.x][crt.y] = FREE;

            for (Node node : expand(board, crt)) {
                queue.offer(node);
            }
        }
    }

    private List<Node> expand(char[][] board, Node node) {
        List<Node> expansion = new ArrayList<Node>();

        for (int i = 0; i < directionX.length; i++) {
            int x = node.x + directionX[i];
            int y = node.y + directionY[i];

            // check validity
            if (x >= 0 && x < board.length && y >= 0 && y < board[0].length && board[x][y] == 'O') {
                board[x][y] = TRAVELED;
                expansion.add(new Node(x, y));
            }
        }

        return expansion;
    }

    static class Node {
        int x;
        int y;

        Node(int x, int y) {
            this.x = x;
            this.y = y;
        }
    }
}
```



