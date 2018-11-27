# House Robber

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and**it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight**without alerting the police**.

### Example

Given`[3, 8, 4]`, return`8`.

### Note

这是一道典型的序列型的动态规划。f\[i\]代表路过完第i家的时候， 最多能有多少钱。一般求什么，f\[i\]就是什么。  
对于i=n的时候，我们有两个选择， 就是抢或者不抢：

* 抢的话，最后是i=n-2的钱数加上第n家的钱数
* 不抢的话， 钱数等于i=n-1的钱数

**2D:**

```java
public int rob(int[] num) {  
    int[][] dp = new int[num.length + 1][2];  
    for (int i = 1; i <= num.length; i++) {  
        dp[i][0] = Math.max(dp[i - 1][0], dp[i - 1][1]);  
        dp[i][1] = num[i - 1] + dp[i - 1][0];  
    }  
    return Math.max(dp[num.length][0], dp[num.length][1]);  
}
```

dp这个二维数组代表盗窃前i栋房子带来的最大收益，其中第二维一共有两个选择分别是0和1。0代表不盗窃第i栋房子，1代表盗窃第i栋房子。换句话就是说，dp\[i\]\[0\]代表盗窃前i栋房子的最大收益，但是不包括第i栋房子的（因为没有盗窃第i栋房子），而dp\[i\]\[0\]代表盗窃前i栋房子的最大收益，其中包括了第i栋房子的（因为第i栋房子被盗窃了）。

其实对一栋房子来说，结果无非是两种，被盗窃和没被窃。所以说，才会有之前分0和1两种情况进行讨论。如果第i栋房子没被盗窃的话，那么dp\[i\]\[0\] = dp\[i-1\]\[0\]和dp\[i-1\]\[1\]中的最大值。这个比较好理解，如果第i栋房子没被窃，那么最大总收益dp\[i\]\[0\]一定和dp\[i-1\]\[0\]，dp\[i-1\]\[1\]这两个之中最大的相同。而假若第i栋房子被窃，那么dp\[i\]\[1\]一定等于第num\[i-1\]（注意，这里的i是从1开始的，所以i－1正好对应num中的第i项，因为num中的index是从0开始的）＋dp\[i-1\]\[0\]，因为第i栋房子已经被窃了，第i－1栋房子肯定不能被窃，否则会触发警报，所以我们只能取dp\[i-1\]\[0\]即第i－1栋房子没被窃情况的最大值。循环结束，最后返回dp\[num.length\]\[0\]和dp\[nums.length\]\[1\]较大的一项。

数组\[80, 7, 9, 90, 87\]按上面的做法得到每步的结果, 选i和不选i的结果

```
       80      7      9      90      87
不选i   0     (80)    80      89     80+90
选i   (80)     7     (89)   (80+90) (87+89)
```

换点数字和顺序:

```
       80      9      7       3      60
不选i   0     (80)    80      87      87
选i   (80)     9     (87)   (80+3) (87+60)
```

我们发现, 对于每一个i, 影响后面能用到的, 只有选i和不选i两个决策结果中比较大的那个, 所以我们可以只存一个, f\[i\]代表路过完第i家的时候， 最多能有多少钱. 就是以下算法:

**1D:**

```java
public class Solution {
    /**
     * @param A: An array of non-negative integers.
     * return: The maximum amount of money you can rob tonight
     */
    //---方法一---
    public long houseRobber(int[] A) {
        // write your code here
        int n = A.length;
        if (n == 0)
            return 0;
        long []res = new long[n+1];


        res[0] = 0;
        res[1] = A[0];
        for (int i = 2; i <= n; i++) {
            res[i] = Math.max(res[i-1], res[i-2] + A[i-1]);
        }
        return res[n];
    }
}
```

之后呢， 我们发现， 对于某个状态c，假设它是奇数位的状态， 它前面有奇状态a和偶状态b：

```
 ...  a       b       c  ...
 ... 奇1     偶1      奇2  ...
```

它的状态只和它前面的一个奇状态和一个偶状态有关, 所以我们可以只存三个变量:

```
         奇1 和 偶1 推出 奇2
```

可是由于在奇2状态结果一出现的时候, 奇1结果就没啥用了, 可以被立即替换, 所以我们就可以只存一对奇偶的状态, 即两个变量, 如下:

滚动**数组**：

```java
public long houseRobber(int[] A) {
        // write your code here
        int n = A.length;
        if (n == 0)
            return 0;
        long []res = new long[2];

        res[0] = 0;
        res[1] = A[0];
        for (int i = 2; i <= n; i++) {
            res[i%2] = Math.max(res[(i-1)%2], res[(i-2)%2] + A[i-1]);
        }
        return res[n%2];
    }
}
```

这就是滚动数组, 或者叫做滚动指针的空间优化.

**利用常量进行滚动**：

```java
public long houseRobber(int[] A) {
    // write your code here
    int n = A.length;
    if (n == 0)
        return 0;

    long twoPrev = 0;
    long onePrev = A[0];
    for (int i = 2; i <= n; i++) {
        long curr = Math.max(onePrev, twoPrev + A[i - 1]);
        twoPrev = onePrev;
        onePrev = curr;
    }
    return onePrev;
}
```



