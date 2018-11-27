# Backpack IV

Given n items with size`nums[i]`which an integer array and all positive numbers, no duplicates. An integer`target`denotes the size of a backpack. Find the number of possible fill the backpack.

`Each item may be chosen unlimited number of times`

### Example

Given candidate items`[2,3,6,7]`and target`7`,

```
A solution set is: 
[7]
[2, 2, 3]
```

return`2`

### Note

```
给出 n 个物品，以及一个数组，nums[i] 代表第 i 个物品的大小，保证大小均为正数并且没有重复，正整数 target 表示背包的大小，找到能填满背包的方案数。
注意事项：每一个物品可以使用无数次。
```

这道题每个物品可以无限次取, 是个无限背包问题.

有N种物品，一个容量为V的背包，每种物品都有无限件可用。第ii种物品的体积为cap\[i\]，价值为val\[i\]。求在不超过背包的容量限制的情况下所能获得的最大总价值和为多少？

这个问题与 0-1 背包和多重背包都不同，前者每种物品只有1件，后者每种物品有num\[i\]件。而对于完全背包来讲，每种物品有无限件。

我们一般把形如这样的背包问题称作完全背包问题。

这个问题仍然可以转化为多重背包问题进行求解？

虽然题目声称每种物品都有无限件，但实际上每种物品最多有V / cap\[i\]件，因此这个问题相当于一个num\[i\] = V / cap\[i\]的多重背包问题。

```
设 backpack[i][j] 代表前 i 个物品选则若干个，所选物品体积恰为 j 的方案数，则有状态转移方程：

backpack[i][j] = backpack[i - 1][j - k * nums[i]]
backpack[0][0] = 1
backpack[0][i] = 0
```

```java
public class Solution {
    /**
     * @param nums an integer array and all positive numbers, no duplicates
     * @param target an integer
     * @return an integer
     */
    public int backPackIV(int[] nums, int target) {
        // Write your code here
        int m = target;
        int []A = nums;
        int f[][] = new int[A.length + 1][m + 1];

        f[0][0] = 1;
        for (int i = 1; i <= A.length; i++) {
            for (int j = 0; j <= m; j++) {
                int k = 0; 
                while(k * A[i-1] <= j) {
                    f[i][j] += f[i-1][j - A[i-1] * k];
                    k += 1;
                }
            } // for j
        } // for i    
        return f[A.length][target];
    }
}
```



