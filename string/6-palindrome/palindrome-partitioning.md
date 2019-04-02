# [Palindrome Partitioning](https://leetcode.com/problems/palindrome-partitioning/description/)

Given a string_s_, partition_s_such that every substring of the partition is a palindrome.

Return all possible palindrome partitioning of_s_.

### **Example**

```
Input:
 "aab"

Output:

[
  ["aa","b"],
  ["a","a","b"]
]
```

### Note



### Code

```java
class Solution {
    public List<List<String>> partition(String s) {
        List<List<String>> res = new ArrayList<>();
        List<String> list = new ArrayList<>();
        
        if (s == null || s.length() == 0) {
            return res;
        }
        
        helper(s, list, res, 0);
        
        return res;
    }
    
    private void helper(String s, 
                        List<String> list,
                        List<List<String>> res,
                        int start) {
        if (start == s.length()) {
            res.add(new ArrayList<String>(list));
            return;
        }
        
        for (int i = start; i < s.length(); i++) {
            String ss = s.substring(start, i + 1);
            if (!isPalindrome(ss)) {
                continue;
            }
            
            list.add(ss);
            helper(s, list, res, i + 1);
            list.remove(list.size() - 1);
        }
    }
    
    private boolean isPalindrome(String s) {
        for (int i = 0, j = s.length() - 1; i < j; i++, j--) {
            if (s.charAt(i) != s.charAt(j)) {
                return false;
            }
        }
        return true;
    }
}
```



