### Backpack II

Given_n\_items with size Aiand value Vi, and a backpack with size\_m_. What's the maximum value can you put into the backpack?

### Example

Given 4 items with size`[2, 3, 5, 7]`and value`[1, 5, 2, 4]`, and a backpack with size`10`. The maximum value is`9`.

### Note

给出`n`个物品的体积`A[i]`和其价值`V[i]`，将他们装入一个大小为`m`的背包，最多能装入的总价值有多大？

> 注意事项：`A[i]`,`V[i]`,`n`,`m`均为整数。你不能将物品进行切分。你所挑选的物品总体积需要小于等于给定的`m`。

可以发现这是一个“裸”的 0-1 背包问题，其中`n`相当于N，`m`相当于V，`A[i]`相当于cap\[i\]，`V[i]`相当于val\[i\]，根据上面的模板可以得到代码。

因为在这个问题中，一件物品要么不选，要么选，正好对应于 0-1 两个状态，所以我们一般把形如这样的背包问题称作 **0-1 背包问题**。

![](/assets/backpack01.png)

```java
public class Solution {
    public int backPackII(int m, int[] A, int[] V) {
        int n = A.length;
        int[][] backpack = new int[n + 1][m + 1];
        for (int i = 0; i < n; ++i) {
            for (int j = 0; j <= m; ++j) {
                backpack[i + 1][j] = backpack[i][j];
                if (j >= A[i]) {
                    backpack[i + 1][j] = Math.max(backpack[i][j], backpack[i][j - A[i]] + V[i]);
                }
            }
        }
        return backpack[n][m];
    }
}
```



