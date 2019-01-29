# [Add Strings](https://leetcode.com/problems/add-strings/description/)

```
Given two non-negative integers num1 and num2 represented as string,
return the sum of num1 and num2.

Note:

- The length of both num1 and num2 is < 5100.
- Both num1 and num2 contains only digits 0-9.
- Both num1 and num2 does not contain any leading zero.
- You must not use any built-in BigInteger library or convert the inputs to integer directly.
```

### Example

”199“ + “1” = “200”

### Note

直接实现吧

如果是浮点数，预处理补位，去掉小数点相加，然后加回小数点

### Code

```java
class Solution {
    public String addStrings(String num1, String num2) {
        if (num1 == null || num2 == null) return "0";
        int len1 = num1.length();
        int len2 = num2.length();
        int carry = 0;
        StringBuilder sb = new StringBuilder();
        while (len1 != 0 || len2 != 0) {
            int v1 = 0, v2 = 0;
            if (len1 != 0) {
                v1 = num1.charAt(len1 - 1) - '0';
                len1--;
            }
            if (len2 != 0) {
                v2 = num2.charAt(len2 - 1) - '0';
                len2--;
            }
            int sum = v1 + v2 + carry;
            carry = sum/10;
            sb.append(sum%10);
        }
        if (carry > 0) {
            sb.append(carry);
        }
        return sb.reverse().toString();
    }
}
```



