# Coins in a Line

There are n coins in a line. Two players take turns to take one or two coins from right side until there are no more coins left. The player who take the last coin wins.

Could you please decide the**first**play will win or lose?

### Example

n =`1`, return`true`.

n =`2`, return`true`.

n =`3`, return`false`.

n =`4`, return`true`.

n =`5`, return`true`.

### Note

博弈有先后手

• State:

先手是否能获胜 / 能够获得的最大利益

• Function:

循环枚举先手的策略可能性

• Intialization:

最极限/最小的状态下的先手的值

• Answer:

整个问题先手是否可能获胜

先思考最小状态

然后思考大的状态-&gt; 往小的递推，那么非常适合记忆化搜索

---

State:

* dp\[i\] 现在还剩i个硬币，现在当前取硬币的人最后输赢状况

Function:

* dp\[i\] = true \(dp\[i-1\]==false 或者 dp\[i-2\]==false\)

Initialize:

* dp\[0\] = false
* dp\[1\] = true
* dp\[2\] = true

Answer:

* dp\[n\]

### Code

```java
public class Solution {
    /**
     * @param n: An integer
     * @return: A boolean which equals to true if the first player will win
     */
    public boolean firstWillWin(int n) {
        // write your code here
        if (n <= 0) {
            return false;
        }
        boolean dp[] = new boolean[2];
        dp[1] = true;

        for (int i = 2; i < n + 1; i++) {
            dp[i % 2] = !(dp[(i -1) % 2] && dp[(i - 2) % 2]);
        }
        return dp[n % 2];
    }
}
```



