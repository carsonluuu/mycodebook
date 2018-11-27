# Coins in a Line II

There are n coins with different value in a line. Two players take turns to take one or two coins from left side until there are no more coins left. The player who take the coins with the most value wins.

Could you please decide the **first **player will win or lose?

### Example

Given values array A =`[1,2,2]`, return`true`.

Given A =`[1,2,4]`, return`false`.

### Note

```
                         [5,1,2,10] 
        先手拿       1(5) /        \ 2(6) 
                    [1,2,10]       [2,10]  
        后手拿   1(1)/    \2(3)  1(2)/  \2(12)
              [2,10]     [10]    [10]  []
```

每次拿硬币的原则不是当前手拿的最多， 而是加上剩下能拿的总共最多。

**基本理解**

**State**:

* dp\[i\] 现在还剩i个硬币，现在先手取硬币的人最后最多取硬币价值

**Function**:

* i 是所有硬币数目
* coin\[n-i\] 表示倒数第i个硬币
* dp\[i\] = max\(min\(dp\[i-2\], dp\[i-3\]\)+coin\[n-i\] \)，\(min\(dp\[i-3\],dp\[i-4\]\)+coin\[n-i\]+coin\[n-i+1\] \)

**Initialize**:

* dp\[0\] = 0
* dp\[1\] = coin\[i-1\]
* dp\[2\] = coin\[i-2\] + coin\[i-1\]
* dp\[3\] = coin\[i-2\] + coin\[i-3\]

**Answer**:

* dp\[n\] &gt; sum/2

---

**使用后缀和数组，bottom-up：**

**State**:

* dp\[i\] 现在还剩i个硬币，现在当前取硬币的人最后最多取硬币价值

**Function**:

* i 是所有硬币数目
* sum\[i\] 是后i个硬币的总和
* dp\[i\] = max\(sum\[i\] - dp\[i-1\], sum\[i\] - dp\[i-2\]\)
* sum\[i\] - dp\[i - 1\] 先手取一个，sum\[i\] - dp\[i - 2\]  先手取二个

**Initialize**:

* dp\[0\] = 0
* dp\[1\] = coin\[i-1\]
* dp\[2\] = coin\[i-2\] + coin\[i-1\]

**Answer**:

* dp\[n\] &gt; sum/2 
* sum\[i\] 代表剩下的这i枚硬币的总价值 sum\[i\] - dp\[i\] 就是对手在还剩i枚硬币的时候开始下手的最大值
* 答案就看dp\[n\]是否大于sum\[n\] - dp\[n\]

**使用后缀和数组，top-down：**

**State**:

* dp\[i\] 表示取 i ~ n-1 这些硬币时，先手取得的最大硬币总价

**Function**:

* sum\[i\] 是后 i ~ n-1 这些硬币的价值总和
* dp\[i\] = max\(sum\[i\] - dp\[i + 1\]\# 先手取一个硬币，sum\[i\] - dp\[i + 2\]\# 先手取两个硬币\)

**Initialization**:

* dp\[n-1\] = coin\[n-1\] \#倒数第一个
* dp\[n-2\] = coin\[n-1\] + coin\[n-2\] \#倒数第一个和倒数第二个

**Answer**:

* dp\[0\]

### Code

```java
public class Solution {
    /**
     * @param values: an array of integers
     * @return: a boolean which equals to true if the first player will win
     */
    public boolean firstWillWin(int[] values) {
        // write your code here
        int n = values.length;
        int[] sum = new int[n + 1];
        for (int i = 1; i <= n; ++i) {
            sum[i] = sum[i -  1] + values[n - i];
        }

        int[] dp = new int[n + 1];
        dp[1] = values[n - 1];
        for (int i = 2; i <= n; ++i) {          
            dp[i] = Math.max(sum[i] - dp[i - 1], sum[i] - dp[i - 2]);
        }

        return dp[n]  > sum[n] / 2;
    }
}
```



