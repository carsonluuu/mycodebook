# [Valid Palindrome](https://leetcode.com/problems/valid-palindrome/description/)

Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

**Note:** For the purpose of this problem, we define empty string as valid palindrome.

### **Example**

**Example 1:**

```
Input:
 "A man, a plan, a canal: Panama"

Output:
 true
```

**Example 2:**

```
Input:
 "race a car"

Output:
 false
```

### Note

双指针，跳过空格

### Code

```java
class Solution {
    public boolean isPalindrome(String s) {
        if (s == null || s.length() == 0) return true;
        int left = 0, right = s.length() - 1;
        while (left < right) {
            while (left < right && !Character.isLetterOrDigit(s.charAt(left))) {
                left++;
            }             
            while (left < right && !Character.isLetterOrDigit(s.charAt(right))) {
                right--;
            }
            if (Character.toLowerCase(s.charAt(left++)) != Character.toLowerCase(s.charAt(right--)))
                return false;
        }
        return true;
    }
}
```



