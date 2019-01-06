# [Longest Substring Without Repeating Characters](https://www.lintcode.com/problem/longest-substring-without-repeating-characters/description?_from=ladder&&fromId=4)

Given a string, find the length of the longest substring without repeating characters.

### Example

For example, the longest substring without repeating letters for`"abcabcbb"`is`"abc"`, which the length is`3`.

For`"bbbbb"`the longest substring is`"b"`, with the length of`1`.

### Note

最大没有重复字符的滑动窗口，没出现过就一直右边界增加，左边移动的时候再把出现的置回0

###  Code

```java
public class Solution {
    /**
     * @param s: a string
     * @return: an integer
     */
    public int lengthOfLongestSubstring(String s) {
        // write your code here
        int[] set = new int[256];
        int res = 0, len = s.length();
        
        int j = 0;
        for (int i = 0; i < len; i++) {
            while (j < len && set[s.charAt(j)] == 0) {
                set[s.charAt(j)]++;
                j++;
            }

            res = Math.max(res, j - i);
            set[s.charAt(i)] = 0;
        }
        
        return res;
    }
}
```



