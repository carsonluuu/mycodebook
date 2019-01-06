# [Find All Anagrams in a String](https://leetcode.com/problems/find-all-anagrams-in-a-string/description/)

Given a string **s **and a **non-empty **string **p**, find all the start indices of **p**'s anagrams in **s**.

Strings consists of lowercase English letters only and the length of both strings **s **and **p **will not be larger than 20,100.

The order of output does not matter.

### Example

**Example 1:**

```
Input:
s: "cbaebabacd" p: "abc"

Output:
[0, 6]

Explanation:
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".
```

**Example 2:**

```
Input:
s: "abab" p: "ab"

Output:
[0, 1, 2]

Explanation:
The substring with start index = 0 is "ab", which is an anagram of "ab".
The substring with start index = 1 is "ba", which is an anagram of "ab".
The substring with start index = 2 is "ab", which is an anagram of "ab".
```

### Note

同上一题的吧

### Code

```java
class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        List<Integer> res = new ArrayList<>();
        if (s == null || s.length() == 0 || p == null || p.length() == 0) return res;
        int len = p.length();
        int[] set = new int[26];
        for (char c : p.toCharArray()) {
            set[c - 'a']++;
        }
        /*
        cbaebabacd
         abc
        */
        int left = 0, right = 0, matched = 0;
        while (right < s.length()) {
            if (set[s.charAt(right) - 'a'] >= 1) {
                matched++;
            }
            set[s.charAt(right) - 'a']--;
            right++;

            if (matched == len) {
                res.add(left);
            }

            if (right - left == len) {
                if (set[s.charAt(left) - 'a'] >= 0) { 
                    matched--; //substract back
                }
                set[s.charAt(left) - 'a']++; //plus back
                left++;
            }
        }

        return res;
    }
}
```



