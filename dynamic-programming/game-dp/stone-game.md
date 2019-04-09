# [Stone Game](https://www.lintcode.com/problem/stone-game/description?_from=ladder&&fromId=4)

There is a stone game.At the beginning of the game the player picks`n`piles of stones in a line.

The goal is to merge the stones in one pile observing the following rules:

1. At each step of the game,the player can merge two adjacent piles to a new pile.
2. The score is the number of stones in the new pile.

You are to determine the minimum of the total score.

### Example

**Example 1:**

```
Input: [3, 4, 3]
Output: 17
```

**Example 2:**

```
Input: [4, 1, 1, 4]
Output: 18
Explanation:
  1. Merge second and third piles => [4, 2, 4], score = 2
  2. Merge the first two piles => [6, 4]，score = 8
  3. Merge the last two piles => [10], score = 18
```

###  Note

贪心反例：\[6,4,4,6\]  
死胡同：容易想到的一个思路从小往大，枚举第一次合并是在哪？

记忆化搜索的思路，从大到小，先考虑最后的0-n-1 合并的总花费

• State: dp\[i\]\[j\] 表示把第i到第j个石子合并到一起的最小花费

• Function: 预处理sum\[i,j\] 表示i到j所有石子价值和: dp\[i\]\[j\] = min\(dp\[i\]\[k\]+dp\[k+1\]\[j\]+sum\[i,j\]\) 对于所有k属于{i,j-1}

• Intialize: For each i that dp\[i\]\[i\] = 0

• Answer: dp\[0\]\[n-1\]

 总结：区间动态规划

* 设定状态: f\[i\]\[j\] 表示合并原序列 \[i, j\] 的石子的最小分数
* 状态转移:`f[i][j] = min{f[i][k] + f[k+1][j]} + sum[i][j], sum[i][j] 表示原序列[i, j]区间的重量和`
* 边界:`f[i][i] = sum[i][i], f[i][i+1] = sum[i][i+1]`
* 答案:`f[0][n-1]`

### Code

```java
public class Solution {
    /**
     * @param A: An integer array
     * @return: An integer
     */
    public int stoneGame(int[] A) {
        // write your code here
        if (A == null || A.length == 0) {
            return 0;
        }
        
        int len = A.length;
        int[][] dp = new int[len][len];
        int[][] visited = new int[len][len];
        
        for (int i = 0; i < len; i++) {
            dp[i][i] = 0;
        }
        
        int[][] sum = new int[len][len];
        for (int i = 0; i < len; i++) {
            sum[i][i] = A[i];
            for (int j = i + 1; j < len; j++) {
                sum[i][j] = sum[i][j - 1] + A[j];
            }
        }
        
        return dfs(0, len - 1, dp, visited, sum);
    }
    
    private int dfs(int start, int end, 
                    int[][] dp, int[][] visited, int[][] sum) {
        if (start >= end) {
            visited[start][end] = 1;
            return dp[start][end];
        }                    
        
        if (visited[start][end] == 1) {
            return dp[start][end];
        }
        
        dp[start][end] = Integer.MAX_VALUE;
        for (int k = start; k < end; k++) {
            dp[start][end] = Math.min(dp[start][end], 
                                      dfs(start, k, dp, visited, sum) +
                                      dfs(k + 1, end, dp, visited, sum) +
                                      sum[start][end]);
        }
        
        visited[start][end] = 1;
        return dp[start][end];
    }
}
```



