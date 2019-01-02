# [Decode String](https://www.lintcode.com/problem/decode-string/description)

Given an expression`s`includes numbers, letters and brackets. Number represents the number of repetitions inside the brackets\(can be a string or another expression\)．Please expand expression to be a string.

### Example

s =`abc3[a]`return`abcaaa`  
s =`3[abc]`return`abcabcabc`  
s =`4[ac]dy`, return`acacacacdy`  
s =`3[2[ad]3[pf]]xyz`, return`adadpfpfpfadadpfpfpfadadpfpfpfxyz`

### Note

两个栈，一个存数字，一个存String

* 遇到数字，读取数字
* 遇到字符，读取字符串
* 遇到 “ \[ ”，压入数字入栈，count归0，压入字符串入栈，字符串归空
* 遇到 “ \] "，数字出栈，字符串出栈，重复数字次，即为新的字符串

### Code

```java
public class Solution {
    
    // https://leetcode.com/problems/decode-string/description/
    
    /**
     * @param s: an expression includes numbers, letters and brackets
     * @return: a string
     */
    public String expressionExpand(String s) {
        // write your code here
        if (s == null) {
            return null;
        }
        if (s.equals("")) {
            return "";
        }
        Stack<StringBuilder> ss = new Stack<>();
        Stack<Integer> sc = new Stack<>();
        StringBuilder curr = new StringBuilder();
        int count = 0;
        for (char c : s.toCharArray()) {
            if (Character.isDigit(c)) {
                count = count * 10 + (c - '0');
            } else if (c == '[') {
                sc.push(count);
                count = 0;
                ss.push(curr);
                curr = new StringBuilder();
            } else if (c == ']') {
                int num = sc.pop();
                StringBuilder temp = new StringBuilder();
                temp.append(ss.pop());
                while (num-- > 0) {
                    temp.append(curr);
                }
                curr = temp;
            } else {
                curr.append(c);
            }
        }
        return curr.toString();
    }
}
```



