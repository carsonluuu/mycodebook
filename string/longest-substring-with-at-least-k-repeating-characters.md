# Longest Substring with At Least K Repeating Characters

Find the length of the longest substring **T **of a given string \(consists of lowercase letters only\) such that every character in **T **appears no less than k times.

### Example

**Example 1:**

```
Input:
s = "aaabb", k = 3

Output:
3

The longest substring is "aaa", as 'a' is repeated 3 times.
```

**Example 2:**

```
Input:
s = "ababbc", k = 2

Output:
5

The longest substring is "ababb", as 'a' is repeated 2 times and 'b' is repeated 3 times.
```

### Note

Divided and Conquer

核心点是：要求的是substring，因此，如果发现一个string中间有一个char是小于k次的，那么最长的substring只可能是这个char左右两边的两个substring

第一步，统计当前string中每个字符出现的次数，用少于k次的字符作为分隔符，把string分割成几个substring，只有这些substring才有可能是满足条件的substring  
第二步，recurse on substrings，找到结果中最大的一个即可，注意当substring数组只有一个元素的时候，直接return其长度，作为一个出口。否则会爆栈。  
终止条件：substring长度已经小于k，substring已空，或 k&lt;=1的时候都可以直接返回确定值了。

### Code

```java
class Solution {
    public int longestSubstring(String s, int k) {
        if (s == null || s.length() == 0) return 0;
        if (k <= 1) return s.length();
        if (s.length() < k) return 0;
        int res = 0;
        Map<Character, Integer> map = new HashMap<>();
        for (int i = 0; i < s.length(); i++) {
            map.put(s.charAt(i), map.getOrDefault(s.charAt(i), 0) + 1);
        }

        StringBuilder sb = new StringBuilder(s);
        for (int i = 0; i < s.length(); i++) {
            if (map.get(s.charAt(i)) < k) {
                sb.setCharAt(i, '#');
            }
        }

        String[] partitions = sb.toString().split("#");
        if (partitions.length == 1) {
            return partitions[0].length();
        }
        for (String str : partitions) {
            res = Math.max(res, longestSubstring(str, k));
        }

        return res;
    }
}
```



