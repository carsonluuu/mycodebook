# [Decode Ways](https://leetcode.com/problems/decode-ways/description/)

A message containing letters from`A-Z`is being encoded to numbers using the following mapping:

```
'A' -> 1
'B' -> 2
...
'Z' -> 26
```

Given a **non-empty **string containing only digits, determine the total number of ways to decode it.

### Example

**Example 1:**

```
Input:
 "12"

Output:
 2

Explanation:
 It could be decoded as "AB" (1 2) or "L" (12).
```

**Example 2:**

```
Input:
 "226"

Output:
 3

Explanation:
 It could be decoded as "BZ" (2 26), "VF" (22 6), or "BBF" (2 2 6).
```

### Note

DP其实更好理解，每次看一位和两位，就是两个情况，满足就加上，不停向前递推

### Code

```java
public int numDecodings(String s) {
    if (s == null || s.length() == 0) return 0;
    int len = s.length();
    int [] dp = new int[len + 1];
    dp[0] = 1;
    dp[1] = s.charAt(0) == '0' ? 0 : 1;
    for (int i = 2; i <= len; i++) {
        int first  = Integer.valueOf(s.substring(i - 1, i));
        int second = Integer.valueOf(s.substring(i - 2, i));
        if (first >= 1 && first <= 9)
            dp[i] += dp[i - 1];
        if (second >= 10 && second <= 26)
            dp[i] += dp[i - 2];
    }
    return dp[len];
}
```

```java
public int numDecodings(String s) {
    if (s == null || s.length() == 0) return 0;
    int len = s.length();

    //ans from i-th position
    int[] memo = new int[len];

    return helper(s, 0, memo);
}

private int helper(String s, int start, int[] memo) {
    if (start == s.length()) {
        return 1;
    }
    if (memo[start] > 0) {
        return memo[start];
    }

    if (s.charAt(start) - '0' == 0) {
        return memo[start];
    } 

    int res = 0;
    for (int i = start; i < start + 2 && i < s.length(); i++) {
        String prefix = s.substring(start, i + 1);
        if (Integer.parseInt(prefix) > 26) {
            continue;
        }
        res += helper(s, i + 1, memo);
    }

    return res;
}
```



