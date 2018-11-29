# [Is Subsequence](https://leetcode.com/problems/is-subsequence/description/)

Given a string**s**and a string**t**, check if**s**is subsequence of**t**.

You may assume that there is only lower case English letters in both**s**and**t**.**t**is potentially a very long \(length ~= 500,000\) string, and **s **is a short string \(&lt;=100\).

A subsequence of a string is a new string which is formed from the original string by deleting some \(can be none\) of the characters without disturbing the relative positions of the remaining characters. \(ie,`"ace"`is a subsequence of`"abcde"`while`"aec"`is not\).

**Example 1:**  
**s**=`"abc"`, **t**=`"ahbgdc"`

Return`true`.

**Example 2:**  
**s**=`"axc"`, **t**=`"ahbgdc"`

Return`false`.

**Follow up:**  
If there are lots of incoming S, say S1, S2, ... , Sk where k &gt;= 1B, and you want to check one by one to see if T has its subsequence. In this scenario, how would you change your code?

### Note

同向双指针分别指向两个字符串

### Code

```java
class Solution {
    public boolean isSubsequence(String s, String t) {
        int i = 0, j = 0;
        if (s.length() > t.length()) {
            return false;
        }

        while (i < s.length() && j < t.length()) {
            if (s.charAt(i) == t.charAt(j)) {
                i++;
            }
            j++;
        }

        return i == s.length();
    }
}
```



