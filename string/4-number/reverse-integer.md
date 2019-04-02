# [Reverse Integer](https://leetcode.com/problems/reverse-integer/description/)

Given a 32-bit signed integer, reverse digits of an integer.

**Example 1:**

```
Input:
 123

Output:
 321

```

**Example 2:**

```
Input:
 -123

Output:
 -321

```

**Example 3:**

```
Input:
 120

Output:
 21

```

**Note:**  
Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: \[−231,  231 − 1\]. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.



### Note

数位分离，注意要求overflow返回0

### Code

```java
class Solution {
    public int reverse(int x) {
        int result = 0;
        int tail, newresult;
        while (x != 0) {
            tail = x % 10;
            newresult = result*10 + tail;
            if ((newresult - tail) / 10 != result)
                return 0;
            result = newresult;
            x = x / 10;
        }
        return result;
    }
}
```



