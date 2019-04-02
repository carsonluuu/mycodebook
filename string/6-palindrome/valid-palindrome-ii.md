# [Valid Palindrome II](https://leetcode.com/problems/valid-palindrome-ii/description/)

Given a non-empty string`s`, you may delete**at most**one character. Judge whether you can make it a palindrome.

### Example

**Example 1:**

```
Input:
 "aba"

Output:
 True
```

**Example 2:**

```
Input:
 "abca"

Output:
 True

Explanation:
 You could delete the character 'c'.
```

### Note

在不一致的情况下，删左边或者删右边，继续判断

```
 return isSubPalindrome(s, start + 1, end) ||
        isSubPalindrome(s, start, end - 1);
```

### Code

```java
class Solution {
    public boolean validPalindrome(String s) {
        int start = 0, end = s.length() - 1;
        while (start < end) {
            if (s.charAt(start) == s.charAt(end)) {
                start++;
                end--;
            } else {
                break;
            }
        }
        
        if (start >= end) {
            return true;
        }
        
        return isSubPalindrome(s, start + 1, end) ||
               isSubPalindrome(s, start, end - 1);
    }
    
    private boolean isSubPalindrome(String s, int start, int end) {
        while (start < end) {
            if (s.charAt(start++) != s.charAt(end--)) {
                return false;
            } 
        }
        
        return true;
    }
}
```



