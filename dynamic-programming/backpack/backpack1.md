# Backpack

Given\_n\_items with size Ai, an integer\_m\_denotes the size of a backpack. How full you can fill this backpack?

### Example

If we have`4`items with size`[2, 3, 5, 7]`, the backpack size is 11, we can select`[2, 3, 5]`, so that the max size we can fill this backpack is`10`. If the backpack size is`12`. we can select`[2, 3, 7]`so that we can fulfill the backpack.

You function should return the max size we can fill in the given backpack.

### Note

我们把每个物品的大小当作每个物品的价值

状态转移是放还是不放，注意要判断内层循环的value值是不是比外层循环对于的物品值大

否则直接是之前状态的值延续`dp[i + 1][j] = dp[i][j]`

外层循环0到i不包括，i状态写i+1状态，内层循环0到最大限制（包括）

### Code

```java
// 一种解法
public class Solution {
    /**
     * @param m: An integer m denotes the size of a backpack
     * @param A: Given n items with size A[i]
     * @return: The maximum size
     */
    public int backPack(int m, int[] A) {
        // write your code here
        int n = A.length;
        int[][] dp = new int[n + 1][m + 1];
        //n is numbers of item, m is size, value is max No.items
        for (int i = 0; i < n; ++i) {
            for (int j = 0; j <= m; ++j) {
                dp[i + 1][j] = dp[i][j];
                if (j >= A[i]) {
                    dp[i + 1][j] = Math.max(dp[i][j], 
                                            dp[i][j - A[i]] + A[i]);
                }
            }
        }
        return dp[n][m];
    }
}

// * O(m) 空间复杂度的解法
public class Solution {
    /**
     * @param m: An integer m denotes the size of a backpack
     * @param A: Given n items with size A[i]
     * @return: The maximum size
     */

    public int backPack(int m, int[] A) {
        int f[] = new int[m + 1];

        for (int i = 0; i < A.length; i++) {
            for (int j = m; j >= A[i]; j--) {
                f[j] = Math.max(f[j], f[j - A[i]] + A[i]);
            } 
        }
        return f[m];
    }
}
```



