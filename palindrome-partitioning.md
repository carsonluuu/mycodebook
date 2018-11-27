# Palindrome Partitioning

Given a string_s_, partition\_s\_such that every substring of the partition is a palindrome.

Return all possible palindrome partitioning of s.

### Example

Given s =`"aab"`, return:

```
[
  ["aa","b"],
  ["a","a","b"]
]
```

### Note

利用backtracking枚举各种情况，和Split String类似，不过这里不是1或者2长度了，两种写法，暴力判断一下是不是回文的

Time complexity: O\(n\*\(2^n\)\)

Space complexity: O\(\(2^n\)\)

DP可以大大提速到大约n平方级别的复杂度

### Code

```java
public class Solution {
    /*
     * @param s: A string
     * @return: A list of lists of string
     */
    public List<List<String>> partition(String s) {
        // write your code here
        List<List<String>> res = new ArrayList<>();
        List<String> partition = new ArrayList<>();

        if (s == null || s.length() == 0) {
            return res;
        }

        //helper(s, partition, res, 0);
        dfs(s, partition, res);

        return res;
    }

    private void dfs(String s, 
                    List<String> partition, 
                    List<List<String>> res) {
        if (s.equals("")) {
            res.add(new ArrayList<String>(partition));
        }                

        for (int i = 0; i < s.length(); i++) {
            String substring = s.substring(0, i + 1);
            if (!isPalindrome(substring)) {
                continue;
            }
            partition.add(substring);
            dfs(s.substring(i + 1), partition, res);
            partition.remove(partition.size() - 1);
        }
    }

    private void helper(String s, 
                        List<String> partition, 
                        List<List<String>> res,
                        int start) {
        if (start == s.length()) {
            res.add(new ArrayList<String>(partition));
        }                    

        for (int i = start; i < s.length(); i++) {
            String substring = s.substring(start, i + 1);
            if (!isPalindrome(substring)) {
                continue;
            }
            partition.add(substring);
            helper(s, partition, res, i + 1);
            partition.remove(partition.size() - 1);
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



