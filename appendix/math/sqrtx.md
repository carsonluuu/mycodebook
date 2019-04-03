```java
public int sqrt(int x) {
    if (x < 0)  throw new IllegalArgumentException();
    else if (x <= 1)    return x;
    int start = 1, end = x;
    // 直接对答案可能存在的区间进行二分 => 二分答案
    while (start + 1 < end) {
        int mid = start + (end - start) / 2;
        // writing in this way instead of "nums[mid] * nums[mid]" to avoid overflow
        if (mid == x / mid)  return mid;
        // possible root must be larger than or equal to current mid
        else if (mid < x / mid) start = mid;
        // possible root must be smaller than or equal to current mid
        else    end = mid;
    }
    if (end > x / end)  return start;
    return end;
}
```

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



