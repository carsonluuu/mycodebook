# Burst Balloons

Given`n`balloons, indexed from`0`to`n-1`. Each balloon is painted with a number on it represented by array`nums`. You are asked to burst all the balloons. If the you burst balloon`i`you will get`nums[left] * nums[i] * nums[right]`coins. Here left and right are adjacent indices of i. After the burst, the left and right then becomes adjacent.

Find the`maximum`coins you can collect by bursting the balloons wisely.

### Example

**Example 1:**

```
Input：[4, 1, 5, 10]
Output：270
Explanation：
nums = [4, 1, 5, 10] burst 1, get coins 4 * 1 * 5 = 20
nums = [4, 5, 10]   burst 5, get coins 4 * 5 * 10 = 200 
nums = [4, 10]    burst 4, get coins 1 * 4 * 10 = 40
nums = [10]    burst 10, get coins 1 * 10 * 1 = 10
Total coins 20 + 200 + 40 + 10 = 270
```

**Example 2:**

```
Input：[3,1,5]
Output：35
Explanation：
nums = [3, 1, 5] burst 1, get coins 3 * 1 * 5 = 15
nums = [3, 5] burst 3, get coins 1 * 3 * 5 = 15
nums = [5] burst 5, get coins 1 * 5 * 1 = 5
Total coins 15 + 15 + 5  = 35
```

* You may imagine`nums[-1] = nums[n] = 1`. They are not real therefore you can not burst them.
* 0 ≤`n`≤ 500, 0 ≤`nums[i]`≤ 100

### Note

  
死胡同：容易想到的一个思路从小往大，枚举第一次在哪吹爆气球？

记忆化搜索的思路，从大到小，先考虑最后一个气球被吹爆之后的获益

将原数组两端加上1 \[4,3,5\] =&gt; \[1,4,3,5,1\]，数组长度 n 从 3 变为 5

• State: dp\[i\]\[j\] 表示把第i+1到第j-1个气球打爆，剩下i,j的最大收益

• Function: 对于所有k属于{i + 1,j - 1}, 表示第k号气球最后打爆。

* score = arr\[i\] \* arr\[k\] \* arr\[j\]
* dp\[i\]\[j\] = max\(dp\[i\]\[k\]+dp\[k\]\[j\]+score\)

• Intialization: dp\[i\]\[i\] = 0

• Answer: dp\[0\]\[n-1\]

区间dp：在区间上进行动态规划，求解一段区间上的最优解。主要是通过合并小区间的 最优解进而得出整个大区间上最优解的dp算法。dp\[i\]\[j\] 代表 burst i+1 ~ j-1 这段时间的所有气球之后，只剩下 i,j 的最大收益。将原来的数组前面和后面增加两个1，最后结果就是 dp\[0\]\[n - 1\]（burst 掉所有气球只剩两个1）

i，i+1以及i+2相邻的3个构成最小的区间，然后k和j移动不断扩大更新区间，利用之前小区间的最优解更新大区间的最优解

### Code

```java
public class Solution {
    public int maxCoins(int[] nums) {
        if (nums == null || nums.length == 0){
            return 0;
        }
        
        nums = init(nums);
        int[][] dp = new int[nums.length][nums.length];
        
        for (int i = nums.length - 1; i >= 0; i--) {
            for (int j = i + 2; j < nums.length; j++) {
                for (int k = i + 1; k < j; k++) {
                    dp[i][j] = Math.max(dp[i][j], dp[i][k] +  dp[k][j] + nums[i] * nums[k] * nums[j]);    //状态转移利用小区间最优解更新大区间
                }
            }
        }
        
        return dp[0][nums.length - 1];
    }
    
    public int[] init(int[] nums){					//初始化数组，头部和尾部插入1
        int[] temp = new int[nums.length + 2];
        temp[0] = 1;
        for(int i = 1; i < temp.length - 1; i++){
            temp[i] = nums[i - 1];
        }
        temp[temp.length - 1] = 1;
        return temp;
    }
}
```



