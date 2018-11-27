# [Knight Dialer](https://leetcode.com/problems/knight-dialer/description/)

A chess knight can move as indicated in the chess diagram below:

![](https://assets.leetcode.com/uploads/2018/10/12/knight.png) .           ![](https://assets.leetcode.com/uploads/2018/10/30/keypad.png)

This time, we place our chess knight on any numbered key of a phone pad \(indicated above\), and the knight makes`N-1`hops.  Each hop must be from one key to another numbered key.

Each time it lands on a key \(including the initial placement of the knight\), it presses the number of that key, pressing`N`digits total.

How many distinct numbers can you dial in this manner?

Since the answer may be large,**output the answer modulo**`10^9 + 7`

### Example

**Example 1:**

```
Input: 1
Output: 10
```

**Example 2:**

```
Input: 2
Output: 20
```

**Example 3:**

```
Input: 3
Output: 46
```

**Note:**

* `1 <= N <= 5000`

### Note

这里给出一个DFS的解法，找到移动的映射之后就可以进行记忆化递归了，传递的参数为步数和当前的字母，枚举每个数字的对应情况，维度就是剩余步数和数字。

Base Case是N=0是结果为1

### Code

```java
class Solution {
    public static final int MOD = 1000000007;
    private static final int[][] graph = 
            new int[][]{{4,6},{6,8},{7,9},{4,8},{3,9,0},{},{1,7,0},{2,6},{1,3},{2,4}};

    public int knightDialer(int N) {
        int res = 0;
        for (int i = 0; i <= 9; i++) {
            res = (res + dfs(N - 1, i, new Integer[N + 1][10])) % MOD;
        }

        return res;
    }

    private int dfs(int N, int start, Integer[][] memo) {
        if (N == 0) {
            return 1;
        }

        if (memo[N][start] != null) {
            return memo[N][start];
        }

        int res = 0;
        for (int nei : graph[start]) {
            res = (res + dfs(N - 1, nei, memo))% MOD;
        }

        memo[N][start] = res;
        return res;
    }
}
```



