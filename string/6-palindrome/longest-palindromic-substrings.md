# [Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/description/)

Given a string**s**, find the longest palindromic substring in**s**. You may assume that the maximum length of**s**is 1000.

**Example 1:**

```
Input: "babad"

Output: "bab"

Note: "aba" is also a valid answer.
```

**Example 2:**

```
Input: "cbbd"

Output: "bb"
```

### Note

DP 

还是注意填充/遍历的顺序，这里是True/False作为值，记录最大的长度

### Code

```java
public String longestPalindrome(String s) {
    String res = "";
    int n = s.length();
    int max = 0;
    boolean[][] dp = new boolean[n][n]; 
    for (int j = 0; j < n; j++) {
        for (int i = 0; i <= j; i++) {
            dp[i][j] = s.charAt(i) == s.charAt(j) && (( j-i < 2)||dp[i+1][j-1]); // i + 1 > j - 1
                
            if (dp[i][j]) {
                if (j - i + 1 > max) {
                max = j - i + 1;
                res = s.substring(i, j + 1);
                }
            }                                
        }
    }
}    
```



