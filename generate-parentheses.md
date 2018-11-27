# [Generate Parentheses](https://leetcode.com/problems/generate-parentheses/)

Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

### Example

For example, givenn= 3, a solution set is:

```
[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```

### Note

这题和二叉树其实挺像的，因为在每一个位置都只有两种可能 "\(" 和 "\)".

left 和 right 都得减到0

递归下去弄，注意退出条件说左边大于右边

### Code

```java
class Solution {
    public static List<String> generateParenthesis(int n) {
        List<String> res = new ArrayList<>();
        if (n == 0) { 
            return res;
        }
        helper(res, "", n, n);
        return res;
    }

    public static void helper(List<String> res, String s, int left, int right) {
        if (left > right) {
            return;
        }
        if (left == 0 && right == 0) {
            res.add(s);
            return;
        }
        if (left > 0) {
            helper(res, s + '(', left - 1, right);
        }
        if (right > 0) {
            helper(res, s + ')', left, right - 1);
        }
    }
}
```



