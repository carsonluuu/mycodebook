# Longest Common Subsequence

Given two strings, find the longest common subsequence \(_LCS_\).

Your code should return the length of _LCS_.

### Example

```
Example 1:
	Input:  "ABCD" and "EDCA"
	Output:  1
	
	Explanation:
	LCS is 'A' or  'D' or 'C'


Example 2:
	Input: "ABCD" and "EACB"
	Output:  2
	
	Explanation: 
	LCS is "AC"
```

### Note

```
if (A.charAt(i - 1) == B.charAt(j - 1)) {
    dp[i][j] = dp[i - 1][j - 1] + 1;
} else {
    dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
}
```

### Code

```java
public class Solution {
    /**
     * @param A: A string
     * @param B: A string
     * @return: The length of longest common subsequence of A and B
     */
    public int longestCommonSubsequence(String A, String B) {
        // write your code here
        if (A == null || B == null || A.length() == 0 || B.length() == 0) {
            return 0;
        }
        
        int m = A.length();
        int n = B.length();
        
        int[][] dp = new int[n + 1][m + 1];
        
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (A.charAt(i - 1) == B.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                } else {
                    dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
                }
            }
        }
        
        return dp[m][n];
    }
}
```

```java
public class Solution {
    /**
     * @param A: A string
     * @param B: A string
     * @return: The length of longest common subsequence of A and B
     */
    public int longestCommonSubsequence(String A, String B) {
        // write your code here
        if (A.isEmpty() || B.isEmpty()) {
            return 0;
        }
        int m = A.length();
        int n = B.length();
        int[][] memo = new int[m+1][n+1];
        for (int i = 0; i <= m; i++) {
            Arrays.fill(memo[i], -1);
        }
        return dfs(A, B, memo, m, n);
    }
    
    private int dfs(String A, String B, int[][] memo, int m, int n) {
        if (memo[m][n] != -1) {
            return memo[m][n];
        }
        
        int result = 0;
        
        if (m == 0 || n == 0) {
            result = 0;
        } else if (A.charAt(m-1) == B.charAt(n-1)) {
            result = dfs(A, B, memo, m-1, n-1) + 1;
        } else {
            result = Math.max(dfs(A, B, memo, m, n-1), dfs(A, B, memo, m-1, n));
        }
        memo[m][n] = result;
        return result;
    }
}
```



