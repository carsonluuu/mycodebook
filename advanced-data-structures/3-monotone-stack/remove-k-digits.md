# [Remove K Digits](https://leetcode.com/problems/remove-k-digits/description/)

Given a non-negative integer num represented as a string, remove k digits from the number so that the new number is the smallest possible.

**Note:**

* The length of num is less than 10002 and will be ≥ k.
* The given num does not contain any leading zero.

### Example

**Example 1:**

```
Input: num = "1432219", k = 3
Output: "1219"
Explanation: Remove the three digits 4, 3, and 2 to form the new number 1219 which is the smallest.
```

**Example 2:**

```
Input: num = "10200", k = 1
Output: "200"
Explanation: Remove the leading 1 and the number is 200. Note that the output must not contain leading zeroes.
```

**Example 3:**

```
Input: num = "10", k = 2
Output: "0"
Explanation: Remove all the digits from the number and it is left with nothing which is 0.
```

### Note

单调递增的栈，但是注意有个k的参数限制

注意几个corner case：

* k就是数字的长度，直接返回“0”
* k在过了单调栈还有的剩，从最后开始删（如111111111）
* 除去头上的零
* 如果k大于num长度，已经清空了stack，这时result为“”，应该返回“0”

### Code

```java
class Solution {
    public String removeKdigits(String num, int k) {
        int len = num.length();
        if (k == len) {
            return "0";
        }
        
        Stack<Character> stack = new Stack<>();
        for (int i = 0; i < len; i++) {
            while (k > 0 && !stack.isEmpty() && stack.peek() > num.charAt(i)) {
                stack.pop();
                k--;
            }
            stack.push(num.charAt(i));
        }
        
        while (k > 0 && !stack.isEmpty()) {
            stack.pop();
            k--;
        }
        
        //construct the number from the stack
        StringBuilder sb = new StringBuilder();
        while (!stack.isEmpty()) {
            sb.append(stack.pop());
        }
        sb.reverse();
        
        //remove all the 0 at the head
        while (sb.length() > 1 && sb.charAt(0) == '0') {
            sb.deleteCharAt(0);
        }
        
        return sb.toString();
    }
}
```



