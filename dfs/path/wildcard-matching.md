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



