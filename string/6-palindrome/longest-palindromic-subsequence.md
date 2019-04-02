# [Longest Palindromic Subsequence](https://leetcode.com/problems/longest-palindromic-subsequence/description/)

Given a string s, find the longest palindromic subsequence's length in s. You may assume that the maximum length of s is 1000.

### **Example**

**Example 1:**  
Input:

```
"bbbab"
```

Output:

```
4
```

One possible longest palindromic subsequence is "bbbb".

**Example 2:**  
Input:

```
"cbbd"
```

Output:

```
2
```

One possible longest palindromic subsequence is "bb".

### Note

注意一下DP矩阵的填充（遍历方式）-- 定长度遍历

### Code

```java
class Solution {
    public int longestPalindromeSubseq(String s) {
        int[][] dp = new int[s.length()][s.length()];
        for (int i = 0; i < s.length(); i++) {
            dp[i][i] = 1;
        }
        for (int d = 1; d < s.length(); d++) {
            for (int i = 0; i < s.length() - d; i++) {
                int j = i + d;
                if (s.charAt(i) == s.charAt(j)) {
                    dp[i][j] = dp[i + 1][j - 1] + 2;
                }
                else{
                    dp[i][j] = Math.max(dp[i + 1][j], dp[i][j - 1]);
                }
            }
        }
        return dp[0][s.length() - 1];
    }
}
```



