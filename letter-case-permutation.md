# [Letter Case Permutation](https://leetcode.com/problems/letter-case-permutation/description/)

Given a string S, we can transform every letter individually to be lowercase or uppercase to create another string.  Return a list of all possible strings we could create.

```
Examples:
Input:
 S = "a1b2"

Output:
 ["a1b2", "a1B2", "A1b2", "A1B2"]


Input:
 S = "3z4"

Output:
 ["3z4", "3Z4"]


Input:
 S = "12345"

Output:
 ["12345"]
```

### Note

```
Time complexity: O(n*2^l), l = # of letters in the string
Space complexity: O(n) + O(n*2^l)
```

### Code

```
class Solution {
    public List<String> letterCasePermutation(String S) {
        List<String> res = new ArrayList<>();
        helper(res, S.toCharArray(), 0);
        return res;
    }
    
    private void helper(List<String> res, char[] c, int pos) {
        if (pos == c.length) {  
            res.add(String.valueOf(c));
            return;
        }
        if (Character.isLetter(c[pos])) {
            c[pos] = Character.toLowerCase(c[pos]);
            helper(res, c, pos + 1);
            c[pos] = Character.toUpperCase(c[pos]);
            helper(res, c, pos + 1);
        } else {
            helper(res, c, pos + 1);
        }
    }
}

```



