# Backpack III

Given_n\_kind of items with size Aiand value Vi\(_`each item has an infinite number available`_\) and a backpack with size\_m_. What's the maximum value can you put into the backpack?

### Example

Given 4 items with size`[2, 3, 5, 7]`and value`[1, 5, 2, 4]`, and a backpack with size`10`. The maximum value is`15`.

### Note

```
给定 n 种具有大小 A[i] 和价值 V[i] 的物品（每个物品可以取用无限次）和一个大小为 m 的一个背包, 你可以放入背包里的最大价值是多少?
注意事项：你不能将物品分成小块, 选择的项目的总大小应小于或等于 m。
```

这道题每个物品可以无限次取, 是个无限背包问题.

有N种物品，一个容量为V的背包，每种物品都有无限件可用。第ii种物品的体积为cap\[i\]，价值为val\[i\]。求在不超过背包的容量限制的情况下所能获得的最大总价值和为多少？

这个问题与 0-1 背包和多重背包都不同，前者每种物品只有1件，后者每种物品有num\[i\]件。而对于完全背包来讲，每种物品有无限件。

我们一般把形如这样的背包问题称作完全背包问题。

这个问题仍然可以转化为多重背包问题进行求解？

虽然题目声称每种物品都有无限件，但实际上每种物品最多有V / cap\[i\]件，因此这个问题相当于一个num\[i\] = V / cap\[i\]的多重背包问题。

### Code

```java
public class Solution {
    public int backPackIII(int[] A, int[] V, int m) {
        int n = A.length;
        int[] f = new int[m + 1];
        for (int i = 0; i < n; ++i) {
            for (int k = 1; k * A[i] <= m; ++k) {
                for (int j = m; j >= A[i]; --j) {
                    f[j] = Math.max(f[j], f[j - A[i]] + V[i]);
                }
            }
        }
        return f[m];
    }
}
```

```
而且优化的方法十分简单，我们只需要将 j 的循环由逆向转变为正向即可。

想一想，为什么？

由于同一种物品的个数无限，所以我们可以在任意容量 j 的背包尝试装入当前物品，j 从小向大枚举可以保证所有包含第 i 种物品，
体积不超过 j - A[i]j−A[i] 的状态被枚举到。

从而得到时间复杂度为 O(mn)，空间复杂度为 O(m) 的优秀算法。
```

```java
//完全背包最优解
public class Solution {
    public int backPackIII(int[] A, int[] V, int m) {
        int n = A.length;
        int[] f = new int[m + 1];
        for (int i = 0; i < n; ++i) {
            for (int j = A[i]; j <= m; ++j) {
                f[j] = Math.max(f[j], f[j - A[i]] + V[i]);
            }
        }
        return f[m];
    }
}
```



