# 动态规划是解决重复子问题的一种方法

_Dynamic Programming is an algorithmic paradigm that solves a given complex problem by breaking it into subproblems and stores the results of subproblems to avoid computing the same results again._

## _**Overlapping Subproblems**_

* _When solutions of same subproblems are needed again and again. In dynamic programming, computed solutions to subproblems are stored in a table so that these don’t have to be recomputed._

## _**Optimal Substructure**_

* _A given problems has Optimal Substructure Property if optimal solution of the given problem can be obtained by using optimal solutions of its subproblems._

### 动态规划四要素 {#动态规划四要素}

**状态 State**

* 灵感，创造力，存储小规模问题的结果
* 最优解/Maximum/Minimum
* Yes/No 存在不存在满足条件的答案
* Count\(\*\) 有多少个可行解

**方程 Function**

* 状态之间的联系，怎么通过小的状态，来求得大的状态

**初始化 Intialization**

* 最极限的小状态是什么, 起点

**答案 Answer**

* 最大的那个状态是什么，终点

### 状态的六大问题: {#状态的六大问题}

1. 坐标型15%
   ```
    jump game: 棋盘，格子
    f[i]代表从起点走到i坐标
   ```
2. 序列型30%
   ```
   f[i]代表前i个元素总和，i=0表示不取任何元素
   ```
3. 双序列型30%
4. 划分型10%
5. 背包型10%
6. 区间型5%

### 滚动数组优化

```
f[i] = max(f[i-1], f[i-2] + A[i]);
```

转换为

```
f[i%2] = max(f[(i-1)%2]和 f[(i-2)%2])
```

### 记忆化搜索

记忆搜索本质是：动态规划

* 动态规划就是解决了重复计算的搜索

动态规划的实现方式：

* 循环（从小到大递推）
* 记忆化搜索\(从大到小搜索\)

记忆化搜索

* 画搜索树
* 万金油搜索可以解决一切问题

* 记忆化搜索可以解决一切动态规划的问题，动态规划都可以用记忆化搜索解决， 但是记忆化搜索不一定是最优解

### 什么时候用记忆化搜索呢?

1. 状态转移特别麻烦, 不是顺序性
2. 初始化状态不是特别容易找到

这时候我们用万能的dfs加memorization  
![](https://i1.wp.com/stomachache007.files.wordpress.com/2017/10/snipaste_20171031_180253.png?ssl=1&w=450 "enter image description here")

#### 那怎么根据DP四要素转化为记忆化搜索呢？ {#那怎么根据dp四要素转化为记忆化搜索呢？}

**State**:

* dp\[x\]\[y\] 以x,y作为结尾的最长子序列

**Function**:

* 遍历x,y 上下左右四个格子

  ```
  dp[x][y] = dp[nx][ny] + 1

  (if a[x][y] > a[nx][ny])
  ```

**Initialize**:

* dp\[x\]\[y\] 是极小值时，初始化为1

**Answer**:

* dp\[x\]\[y\]中最大值

![](https://i2.wp.com/stomachache007.files.wordpress.com/2017/10/snipaste_20171031_180823.png?ssl=1&w=450 "enter image description here")

