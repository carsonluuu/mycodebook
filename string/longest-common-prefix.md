# Longest Common Prefix

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string`""`.

**Example 1:**

```
Input: 
["flower","flow","flight"]

Output:
 "fl"
```

**Example 2:**

```
Input: 
["dog","racecar","car"]

Output:
 ""

Explanation:
 There is no common prefix among the input strings.
```

### Note

利用index of判断是不是含有这个前缀，不包含时一直从后往前减小长度

遍历，维护一个最大的res即为答案，其会是所有的公共前缀

### Code

```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if (strs == null || strs.length == 0 ) return "";
        String res = strs[0];
        for (int i = 1; i < strs.length; i++) {
            while (strs[i].indexOf(res) != 0) {
                res = res.substring(0, res.length() - 1);
            }
        }
        return res;
    }
}
```



