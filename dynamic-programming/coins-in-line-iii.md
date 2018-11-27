# Coins in a Line III

There are\_n\_coins in a line. Two players take turns to take a coin from one of the ends of the line until there are no more coins left. The player with the larger amount of money wins.

Could you please decide the first player will win or lose?

### Example

Given array A =`[3,2,2]`, return`true`.

Given array A =`[1,2,4]`, return`true`.

Given array A =`[1,20,4]`, return`false`.

### Note

区间DP + 博弈DP

来来来, 先画个图:  
![](https://stomachache007.files.wordpress.com/2017/11/evernote-snapshot-20171105-151531-1.png?w=300&h=248 "Evernote Snapshot 20171105 151531 \(1\)")

如图, 我们发现, 一下相同的重复的\[2\], 可以用memo搜索. 但是, 假设我们用一个状态dp\[1\], 我们不知道剩的一个, 是2, 是3还是4啊. 因为现在取一个硬币,可以从左边取, 也可以从右边取, 是有方向性的, 所以不能用dp\[i\]表示.  
现在我们呢, 用一个区间的两个下标表示

State:

* dp\[i\]\[j\] 现在还第i到第j的硬币，现在先手取硬币的人最后最多取硬币价值

Function:

* left = min\(dp\[i+2\]\[j\], dp\[i+1\]\[j-1\]\)+coin\[i\] \[i+1, j\]
* right = min\(dp\[i\]\[j-2\], dp\[i+1\]\[j-1\]\)+coin\[j\] \[i, j-1\]
* dp\[i\]\[j\] = max\(left, right\).

Initialize:

* dp\[i\]\[i\] = coin\[i\],
* dp\[i\]\[i+1\] = max\(coin\[i\],coin\[i+1\]\),

Answer:

* dp\[0\]\[n-1\] &gt; sum/2

OR

State:

* dp\[i\]\[j\] 现在还第i到第j的硬币，现在当前取硬币的人最后最多取硬币价值

Function:

* sum\[i\]\[j\]第i到第j的硬币价值总和 ---- sum\[j  + 1\] - sum\[i\]
* dp\[i\]\[j\] = max\(sum\[i\]\[j\] – dp\[i+1\]\[j\], sum\[i\]\[j\] – dp\[i\]\[j-1\]\);

Initialize:

* dp\[i\]\[i\] = coin\[i\]

Answer:

* dp\[0\]\[n-1\] &gt; sum\[0\]\[n-1\] / 2

我们会发现, 如图

![](https://stomachache007.files.wordpress.com/2017/11/evernote-snapshot-20171105-152835.png?w=300&h=249 "Evernote Snapshot 20171105 152835")

我们是先初始化对角线, 然后往按区间往右上递推的.先黄色的线, 然后蓝色的线, 然后粉色的…

初始化, 就是初始化那些没法递推的.  
从大往小想比较容易想, 可以用for来写, 但是写起来没有递归单独写出一个方程来容易.

* [x] 需要初始化所有的dp\[i\]\[i\] = values\[i\]
* [x] 注意遍历外层循环需要是区间长度（保证之前被填了，这里是区间长度从2变到n）

### Code



