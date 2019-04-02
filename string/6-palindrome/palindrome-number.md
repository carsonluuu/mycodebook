# [Palindrome Number](https://leetcode.com/problems/palindrome-number/description/)

Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.

### Example

**Example 1:**

```
Input:
 121

Output:
 true
```

**Example 2:**

```
Input:
 -121

Output:
 false

Explanation:
 From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
```

**Example 3:**

```
Input:
 10

Output:
 false

Explanation:
 Reads 01 from right to left. Therefore it is not a palindrome.
```

**Follow up:**

Could you solve it without converting the integer to a string?

### Note

数位分离+反转

计算反转一半和半段是不是相等

x是前半段

r是反转的后半段 x == r / 10，x == r 对应奇数和偶数（奇数中间位不判断）

### Code

```java
public boolean isPalindrome(int x) {
    if( x < 0 || (x != 0 && x % 10 == 0)) return false;
    int num = x;
    int r = 0;
    while (x > r) {
        r = r * 10 + x % 10;
        x /= 10;
    }
    return (x == r || x == r / 10);
}
```



