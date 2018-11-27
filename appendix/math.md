```java
public double sqrt(double x) {
    double res = 1.0;
    double eps = 1e-12;

    while (Math.abs(res * res - x) > eps) {
        res = (res + x / res) / 2;
    }

    return res;
}
```

```java
public double sqrt(double x) {
    // Write your code here
    double l = 0; 
    double r = Math.max(x, 1.0);
    double eps = 1e-12;
    
    while (l + eps < r) {
        double mid = (l + r) / 2;
        if (mid * mid < x) {
            l = mid;
        } else {
            r = mid;
        }
    }
    
    return l;
}
```



