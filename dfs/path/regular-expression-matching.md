# [Regular Expression Matching](https://leetcode.com/problems/regular-expression-matching/description/)

Given an input string \(`s`\) and a pattern \(`p`\), implement regular expression matching with support for`'.'`and`'*'`.

```
'.' Matches any single character.
'*' Matches zero or more of the preceding element.
```

The matching should cover the**entire**input string \(not partial\).

**Note:**

* `s`could be empty and contains only lowercase letters`a-z`.
* `p`could be empty and contains only lowercase letters`a-z`, and characters like `.` or`*`.

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
p = "a*"

Output:
 true

Explanation:
 '*' means zero or more of the precedeng element, 'a'. Therefore, by repeating 'a' once, it becomes "aa".
```

**Example 3:**

```
Input:

s = "ab"
p = ".*"

Output:
 true

Explanation:
 ".*" means "zero or more (*) of any character (.)".
这个要注意！s可以为任意字符串
```

**Example 4:**

```
Input:

s = "aab"
p = "c*a*b"

Output:
 true

Explanation:
 c can be repeated 0 times, a can be repeated 1 time. Therefore it matches "aab".
```

**Example 5:**

```
Input:

s = "mississippi"
p = "mis*is*p*."

Output:
 false
```

### Note

分类讨论：

1. 当前字符相同的情况：`sChar == pChar || pChar == '.'` 相同或者pattern字符是"."，s和p都看下一个字符开头的子串

2. p的下一个字符是"\*"的情况：

3. * p向后跳2位，对应"a\*"是空的情况
   * s和p当前字符相同，**并且**s往后跳一个，对应一个或者重复的情况

递归边界：

1. `““ == ”“` 的情况：p到头，s也要到头

2. `“” == "x*x*x*x*x*"` 的情况，s到头，p可以为空 `isEmpty(p, pIndex)`

Memo:

1. 二维boolean数组表示0到index的子串匹配情况

2. visited数组来记录是否在memo里出现

### Code

```java
public class Solution {
    /**
     * @param s: A string 
     * @param p: A string includes "." and "*"
     * @return: A boolean
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
        // "" == ""
        if (pIndex == p.length()) {
            return sIndex == s.length();
        }

        if (sIndex == s.length()) {
            return isEmpty(p, pIndex);
        }

        if (visited[sIndex][pIndex]) {
            return memo[sIndex][pIndex];
        }

        char sChar = s.charAt(sIndex);
        char pChar = p.charAt(pIndex);
        boolean match;

        // consider a* as a bundle
        if (pIndex + 1 < p.length() && p.charAt(pIndex + 1) == '*') {
            match = isMatchHelper(s, sIndex, p, pIndex + 2, memo, visited) ||
                charMatch(sChar, pChar) && isMatchHelper(s, sIndex + 1, p, pIndex, memo, visited);
        } else {
            match = charMatch(sChar, pChar) && 
                isMatchHelper(s, sIndex + 1, p, pIndex + 1, memo, visited);
        }

        visited[sIndex][pIndex] = true;
        memo[sIndex][pIndex] = match;
        return match;
    }

    private boolean charMatch(char sChar, char pChar) {
        return sChar == pChar || pChar == '.';
    }

    private boolean isEmpty(String p, int pIndex) {
        for (int i = pIndex; i < p.length(); i += 2) {
            if (i + 1 >= p.length() || p.charAt(i + 1) != '*') {
                return false;
            }
        }
        return true;
    }
}
```



