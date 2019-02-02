# [Nth Digit](https://leetcode.com/problems/nth-digit/description/)

Find thenthdigit of the infinite integer sequence 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, ...

**Note:**  
nis positive and will fit within the range of a 32-bit signed integer \(n&lt; 231\).

### Example

**Example 1:**

```
Input:

3

Output:

3
```

**Example 2:**

```
Input:
11

Output:
0

Explanation:

The 11th digit of the sequence 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, ... is a 0,
which is part of the number 10.
```

### Note

see code

### Code

```java
class Solution {
    public int findNthDigit(int n) {
        long count = 9;
        int len = 1;
        int start = 1;
        while (n > count * len) {
            n -= count * len;
            len++;
            count *= 10; // 9*1 + 90 * 2 + 900 *3 + ... --> digits
            start *= 10;
        }
        
		start += (n - 1) / len; //start is 10/100/1000 minus 1 for begin with 9/99/999
		String s = Integer.toString(start);
		return Character.getNumericValue(s.charAt((n - 1) % len));
    }
}
```



