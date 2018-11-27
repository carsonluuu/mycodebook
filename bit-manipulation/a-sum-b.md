### Sum of Two Integers

Calculate the sum of two integersaandb, but you are**not allowed**to use the operator`+`and`-`.

**Example 1:**

```
Input: a = 1, b = 2
Output: 3
```

**Example 2:**

```
Input: a = -2, b = 3
Output: 1
```

### Note

For this, problem, for example, we have a = 1, b = 3, In bit representation, a = 0001, b = 0011,

* First, we can use "and"\("&"\) operation between a and b to find a carry. carry = a & b, then carry = 0001
* Second, we can use "xor" \("^"\) operation between a and b to find the different bit, and assign it to a, Then, we shift carry one position left and assign it to b, b = 0010. Iterate until there is no carry \(or b == 0\)

### Code

```java
// Iterative
public int getSum(int a, int b) {
    if (a == 0) return b;
    if (b == 0) return a;

    while (b != 0) {
        int carry = a & b;
        a = a ^ b;
        b = carry << 1;
    }

    return a;
}

// Iterative
public int getSubtract(int a, int b) {
    while (b != 0) {
        int borrow = (~a) & b;
        a = a ^ b;
        b = borrow << 1;
    }

    return a;
}

// Recursive
public int getSum(int a, int b) {
    return (b == 0) ? a : getSum(a ^ b, (a & b) << 1);
}

// Recursive
public int getSubtract(int a, int b) {
    return (b == 0) ? a : getSubtract(a ^ b, (~a & b) << 1);
}

// Get negative number
public int negate(int x) {
    return ~x + 1;
}
```



