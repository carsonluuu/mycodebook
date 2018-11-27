```java
private int _gcd(int A, int B) {
    return b > 0 ? _gcd(b, a % b) : a;
}

private int _lcm(int A, int B) {
    return A * B / _gcd(A, B);
}
```



