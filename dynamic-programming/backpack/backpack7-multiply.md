# Backpack VII

Assume that you have`n`yuan. There are many kinds of rice in the supermarket. Each kind of rice is bagged and must be purchased in the whole bag. Given the`weight`,`price`and`quantity`of each type of rice, find`the maximum weight`of rice that you can purchase.

### Example

```
Given:
n = 8
prices = [2,4]
weight = [100,100]
amounts = [4,2]

Return:400
```

### Note

除了 0-1 背包问题外，还有一种背包问题称作多重背包问题。

> 有N种物品，一个容量为V的背包，第i种物品的数量为num\[i\]，体积为cap\[i\]，价值为val\[i\]，求在不超过背包的容量限制的情况下所能获得的最大物品价值和为多少？

这个问题与 0-1 背包的区别在于，0-1 背包中每种物品有且只有一个，而多重背包中一种物品有nums\[i\]个。我们一般把形如这样的背包问题称作多重背包问题。

求解这个问题一个简单的思路就是可以把它看成一个拥有 ∑num\[i\]件物品的 0-1 背包问题。

另一种简单的思路是将它看成一个拥有N件物品的 0-1 背包问题，但是第i件物品的体积和价值有num\[i\]种取值。

```java
for (int i = 1; i <= N; ++i) {
    for (int j = 0; j <= V; ++j) {
        backpack[i][j] = backpack[i - 1][j];
        for (int k = 1; k <= num[i]; ++k) {
            if (j >= k * cap[i]) {
                backpack[i][j] = Math.max(backpack[i][j], backpack[i - 1][j - k * cap[i]] + k * val[i]);
            }
        }
    }
}
```

```
时间复杂度 O(V∑num[i])，空间复杂度 O(NV)
```

最优解：

```java
for (int i = 1; i <= N; ++i) {
    for (int k = 1; k <= num[i]; ++k) {
        for (int j = V; j >= cap[i]; --j) {
            f[j] = Math.max(f[j], f[j - cap[i]] + val[i]);
        }
    }
}
```

```
时间复杂度O(V∑num[i])，空间复杂度 O(V)
```



