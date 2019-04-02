# [Valid Number](https://leetcode.com/problems/valid-number/description/)

Validate if a given string can be interpreted as a decimal number.

### Example

Some examples:  
`"0"`=&gt;`true`  
`" 0.1 "`=&gt;`true`  
`"abc"`=&gt;`false`  
`"1 a"`=&gt;`false`  
`"2e10"`=&gt;`true`  
`" -90e3   "`=&gt;`true`  
`" 1e"`=&gt;`false`  
`"e3"`=&gt;`false`  
`" 6e-1"`=&gt;`true`  
`" 99e2.5 "`=&gt;`false`  
`"53.5e93"`=&gt;`true`  
`" --6 "`=&gt;`false`  
`"-+3"`=&gt;`false`  
`"95a54e53"`=&gt;`false`

**Note:**It is intended for the problem statement to be ambiguous. You should gather all requirements up front before implementing one. However, here is a list of characters that can be in a valid decimal number:

* Numbers 0-9
* Exponent - "e"
* Positive/negative sign - "+"/"-"
* Decimal point - "."

Of course, the context of these characters also matters in the input.

**Update \(2015-02-10\):**  
The signature of the`C++`function had been updated. If you still see your function signature accepts a`const char *`argument, please click the reload button to reset your code definition.

### Note

计算point和digit的出现次数，point多于1或者digit少于1都不行

对于自然对数，最后再次判断

### Code

```java
class Solution {
    public boolean isNumber(String s) {
        int nPiont = 0, nDigit = 0;
        s = s.trim() + " ";
        char[] c = s.toCharArray();
        int i = 0;
        int len = c.length - 1;
        if (c[i] == '+' || c[i] == '-') {
            i++;
        }
        while (Character.isDigit(c[i]) || c[i] == '.') {
            if (Character.isDigit(c[i])) {
                nDigit++;
            }
            if (c[i] == '.') {
                nPiont++;
            }
            i++;
        }
        if (nPiont > 1) {
            return false;
        }
        if (nDigit < 1) {
            return false;
        }
        if (c[i] == 'e') {
            i++;
            if (c[i] == '+' || c[i] == '-') {
                i++;
            }
            if (i == len) {
                return false;
            }
            for (; i < len; i++) {
                if (!Character.isDigit(c[i])) {
                    return false;
                }
            }
        }
        return i == len;
    }
}

```



