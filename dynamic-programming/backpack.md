## 什么是背包问题？

简单来讲，你有一个背包，它的容量为VV，你同时有若干个物品，它们有各自的体积和价值，将哪些物品装入背包可以使得它们的总体积和不超过背包的容量而总价值和最大？

我们把形如这样的一类与背包有关的问题称为背包问题。

## 有哪些背包问题？

1. 0-1 背包问题 [Backpack](http://www.lintcode.com/zh-cn/problem/backpack/),[Backpack II](http://www.lintcode.com/zh-cn/problem/backpack-ii/),[Backpack V](http://www.lintcode.com/zh-cn/problem/backpack-v/),[Backpack VI](http://www.lintcode.com/zh-cn/problem/backpack-vi/)

2. 多重背包问题 [Backpack VII](http://www.lintcode.com/zh-cn/problem/backpack-vii/),[Backpack VIII](http://www.lintcode.com/zh-cn/problem/backpack-viii/)

3. 完全背包问题 [Backpack III](http://www.lintcode.com/zh-cn/problem/backpack-iii/),[Backpack IV](http://www.lintcode.com/zh-cn/problem/backpack-iv/)

## 背包问题举例

> 有N个物品，一个容量为V的背包，第ii个物品的体积为cap\[i\]，价值为val\[i\]，求在不超过背包的容量限制的情况下所能获得的最大物品价值和为多少？

## 什么是伪多项式时间

> 问题：0-1 背包时间复杂度为O\(VN\)的动态规划解法是多项式时间算法吗？其中，V表示背包容量，N表示物品个数。

这个问题可以说是，也可以说不是。为什么呢？

说是，是因为O\(VN\)，相对于V和N这两个数字值是多项式时间的。

说不是，是因为O\(VN\)，相对于输入所需要的`位`的长度 `O(logV + Nlog(max(cap[i], val[i]))` 是指数时间的。

我们一般把运行时间是关于**输入规模**（输入所需要的位的长度）为指数时间，而关于输入的**数字值**为多项式时间的时间称为伪多项式时间。





