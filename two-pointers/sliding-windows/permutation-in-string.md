# [Permutation in String](https://leetcode.com/problems/permutation-in-string/description/)

Given two strings **s1 **and **s2**, write a function to return true if **s2 **contains the permutation of **s1**. In other words, one of the first string's permutations is the **substring **of the second string.

### Example

**Example 1:**

```
Input:
s1 = "ab" s2 = "eidbaooo"

Output:
True

Explanation:
 s2 contains one permutation of s1 ("ba").
```

**Example 2:**

```
Input:
s1= "ab" s2 = "eidboaoo"

Output:
 False
```

### Note

Fixed length of the window size.

Take the templet one.

### Code

```java
class Solution {
    public boolean checkInclusion(String s1, String s2) {
        int[] set = new int[26];
        for (int i = 0; i < s1.length(); i++) {
            set[s1.charAt(i) - 'a']++;
        }

        int left = 0, right = 0;
        int len = s1.length(), matched = 0;
        while (right < s2.length()) {
            if (set[s2.charAt(right) - 'a'] >= 1) {
                matched++;
            }
            set[s2.charAt(right) - 'a']--;
            right++;

            if (matched == len) {
                return true;
            }

            if (right - left == len) {
                if (set[s2.charAt(left) - 'a'] >= 0) {
                    matched--;
                }
                set[s2.charAt(left) - 'a']++;
                left++;
            }
        }

        return false;
    }
}
```



