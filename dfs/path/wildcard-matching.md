# [Wildcard Matching](https://leetcode.com/problems/wildcard-matching/description/)

Given an input string \(`s`\) and a pattern \(`p`\), implement wildcard pattern matching with support for`'?'`and`'*'`.

```
'?' Matches any single character.
'*' Matches any sequence of characters (including the empty sequence).
```

The matching should cover the **entire **input string \(not partial\).

**Note:**

* `s`could be empty and contains only lowercase letters`a-z`.
* `p`could be empty and contains only lowercase letters`a-z`, and characters like`?` or`*`.

### Example

**Example 1:**

```
Input:

s = "aa"
p = "a"

Output:
 false

Explanation:
 "a" does not match the entire string "aa".
```

**Example 2:**

```
Input:

s = "aa"
p = "*"

Output:
 true

Explanation:
 '*' matches any sequence.
```

**Example 3:**

```
Input:

s = "cb"
p = "?a"

Output:
 false

Explanation:
 '?' matches 'c', but the second letter is 'a', which does not match 'b'.
```

**Example 4:**

```
Input:

s = "adceb"
p = "*a*b"

Output:
 true

Explanation:
 The first '*' matches the empty sequence, while the second '*' matches the substring "dce".
```

**Example 5:**

```
Input:

s = "acdcb"
p = "a*c?b"

Output:
 false
```

### Note

分类讨论：

1. 当前字符相同的情况：`sChar == pChar || pChar == '?'` 相同或者pattern字符是"?"，s和p都看下一个字符开头的子串

2. p是"\*"的情况：

3. * p向后跳1位，对应"a\*"是空的情况
   * s往后跳1位，对应一个或者多个字符序列的情况

递归边界：

1. `““ == ”“` 的情况：p到头，s也要到头

2. `“” == "********"` 的情况，s到头，p必须all star

Memo:

1. 二维boolean数组表示0到index的子串匹配情况

2. visited数组来记录是否在memo里出现

### Code

```java
public class Solution {
    /**
     * @param s: A string 
     * @param p: A string includes "?" and "*"
     * @return: is Match?
     */
    public boolean isMatch(String s, String p) {
        if (s == null || p == null) {
            return false;
        }
        
        boolean[][] memo = new boolean[s.length()][p.length()];
        boolean[][] visited = new boolean[s.length()][p.length()];
        return isMatchHelper(s, 0, p, 0, memo, visited);
    }
    
    private boolean isMatchHelper(String s, int sIndex,
                                  String p, int pIndex,
                                  boolean[][] memo,
                                  boolean[][] visited) {
        // 如果 p 从pIdex开始是空字符串了，那么 s 也必须从 sIndex 是空才能匹配上
        if (pIndex == p.length()) {
            return sIndex == s.length();
        }
        
        // 如果 s 从 sIndex 是空，那么p 必须全是 * 
        if (sIndex == s.length()) {
            return allStar(p, pIndex);
        }
        
        if (visited[sIndex][pIndex]) {
            return memo[sIndex][pIndex];
        }
        
        char sChar = s.charAt(sIndex);
        char pChar = p.charAt(pIndex);
        boolean match;
        
        if (pChar == '*') {
            match = isMatchHelper(s, sIndex, p, pIndex + 1, memo, visited) ||
                isMatchHelper(s, sIndex + 1, p, pIndex, memo, visited);
        } else {
            match = charMatch(sChar, pChar) &&
                isMatchHelper(s, sIndex + 1, p, pIndex + 1, memo, visited);
        }
        
        visited[sIndex][pIndex] = true;
        memo[sIndex][pIndex] = match;
        return match;
    }
    
    private boolean charMatch(char sChar, char pChar) {
        return (sChar == pChar || pChar == '?');
    }
    
    private boolean allStar(String p, int pIndex) {
        for (int i = pIndex; i < p.length(); i++) {
            if (p.charAt(i) != '*') {
                return false;
            }
        }
        return true;
    }
}
```



