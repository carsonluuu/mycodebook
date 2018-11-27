# [Snakes and Ladders](https://leetcode.com/problems/snakes-and-ladders/description/)

On an N x N `board`, the numbers from`1`to`N*N`are written _boustrophedonically _**starting from the bottom left of the board**, and alternating direction each row.

For example, for a 6 x 6 board, the numbers are written as follows:

![](/assets/snakeBoard.png)You start on square`1`of the board \(which is always in the last row and first column\).  Each move, starting from square`x`, consists of the following:

* You choose a destination square`S`with number `x+1`,`x+2`,`x+3`,`x+4`,`x+5`, or`x+6`, provided this number is `<= N*N`.
  * \(This choice simulates the result of a standard 6-sided die roll: ie., there are always at most 6 destinations.\)
* If`S` has a snake or ladder, you move to the destination of that snake or ladder.  Otherwise, you move to`S`.

A board square on row`r`and column`c` has a "snake or ladder" if`board[r][c] != -1`.  The destination of that snake or ladder is`board[r][c]`.

Note that you only take a snake or ladder at most once per move: if the destination to a snake or ladder is the start of another snake or ladder, you do**not**continue moving.  \(For example, if the board is \`\[\[4,-1\],\[-1,3\]\]\`, and on the first move your destination square is \`2\`, then you finish your first move at \`3\`, because you do**not**continue moving to \`4\`.\)

Return the least number of moves required to reach squareN\*N.  If it is not possible, return`-1`.

### **Example**

```
Input: 
[
[-1,-1,-1,-1,-1,-1],
[-1,-1,-1,-1,-1,-1],
[-1,-1,-1,-1,-1,-1],
[-1,35,-1,-1,13,-1],
[-1,-1,-1,-1,-1,-1],
[-1,15,-1,-1,-1,-1]]

Output: 
4

Explanation: 

At the beginning, you start at square 1 [at row 5, column 0].
You decide to move to square 2, and must take the ladder to square 15.
You then decide to move to square 17 (row 3, column 5), and must take the snake to square 13.
You then decide to move to square 14, and must take the ladder to square 35.
You then decide to move to square 36, ending the game.
It can be shown that you need at least 4 moves to reach the N*N-th square, so the answer is 4.
```

### Note

比较tricky，先降维（处理的都减1，方便直接跳转），然后在数组里做BFS找到最短路径，每次可以走最多6步，终点是`N*N - 1`

```
Math.min(curr + 6, N * N - 1)
```

### Code

```java
class Solution {
    public int snakesAndLadders(int[][] board) {
        int N = board.length;
        int[] nums = new int[N * N];
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                if (i % 2 == 0) {
                    nums[i * N + j] = board[N - i - 1][j] - 1;
                } else {
                    nums[i * N + N - j - 1] = board[N - i - 1][j] - 1;
                }
            }
        }

        Queue<Integer> q = new LinkedList<>();
        Set<Integer> set = new HashSet<>();
        q.offer(0);
        set.add(0);
        int res = 0;
        while (!q.isEmpty()) {
            int size = q.size();
            while (size-- > 0) {
                int curr = q.poll();
                if (curr == N * N - 1) {
                    return res;
                }
                for (int i = curr + 1; i <= Math.min(curr + 6, N * N - 1); i++) {
                    int next = nums[i] == -2 ? i : nums[i];
                    if (!set.contains(next)) {
                        q.offer(next);
                        set.add(next);
                    }
                }
            }
            res++;
        }
        return -1;        
    }

}
```



