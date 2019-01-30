# [Divide Two Integers](https://leetcode.com/problems/divide-two-integers/description/)

Given two integers`dividend`and`divisor`, divide two integers without using multiplication, division and mod operator.

Return the quotient after dividing`dividend`by`divisor`.

The integer division should truncate toward zero.

### Example

**Example 1:**

```
Input: dividend = 10, divisor = 3

Output: 3
```

**Example 2:**

```
Input: dividend = 7, divisor = -3

Output: -2
```

### Note

corner case:

* 负数
* 100/0
* 0/2
* 越界

不停减除数然后加一

```java
while ((sum + sum) <= ldividend){
    sum += sum;
    multiple += multiple;
}
```

加等号会少跑一次，无伤大雅

时间空间都是O\(logn\)

### Code

```java
class Solution {
    public int divide(int dividend, int divisor) {
        int sign = 1;
        int res;
        if ((dividend > 0 && divisor < 0) || (dividend < 0 && divisor > 0)) sign = -1;
        long ldividend = Math.abs((long)dividend);
        long ldivisor = Math.abs((long)divisor);
        if(ldividend < ldivisor || ldividend == 0) return 0;

        long lres = divide(ldividend, ldivisor);

        if (lres > Integer.MAX_VALUE){
            res = (sign == 1) ? Integer.MAX_VALUE : Integer.MIN_VALUE;            
        } else res = (int)(sign * lres);

        return res;
    }

    public long divide(long ldividend, long ldivisor){
        if(ldividend < ldivisor) return 0;
        long sum = ldivisor;
        long multiple = 1;
        while ((sum + sum) <= ldividend){
            sum += sum;
            multiple += multiple;
        }
        return multiple + divide(ldividend-sum, ldivisor);
    }
}
```



