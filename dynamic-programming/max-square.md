# Maximal Square

Given a 2D binary matrix filled with 0's and 1's, find the largest square containing all 1's and return its area.

### Example

For example, given the following matrix:

```
1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0
```

Return`4`.

### Note

长方形往往选左上和右下角的角点开始, 正方形一般选右下角.

\(2,3\)这个点为右下角点的square的大小, 其实和\(1,2\)有关, 它最大是\(1,2\)的squre的边长再加一  
那么呢, 我们可以把正方形分成pic5.1图中的几个部分:  
![](https://stomachache007.files.wordpress.com/2017/10/evernote-snapshot-20171031-162349.png?w=300&h=300 "Evernote Snapshot 20171031 162349")  
对于一个点A, 我们需要看看它左上的点最大的正方形边长, 然后验证它左边连续是1的点的长度和上面连续是1的点的长度, 即

```
1. for向左都是1的长度
2. for向上都是1的长度
3. for左上点的最大正方形的边长
```

1, 2和3的值中的最小值+1就是结果

其中1和2可以用预处理过得矩阵left\[\]\[\]和up\[\]\[\]优化.  
这是状态方程是：

```
if matrix[i][j] == 1
    f[i][j] = min(LEFT[i][j-1], UP[i-1][j], f[i-1][j-1]) + 1;
if matrix[i][j] == 0
    f[i][j] = 0
```

接着呢, 我们发现, 其实left和up矩阵是不需要的. 如图pic5.2:  
![](https://stomachache007.files.wordpress.com/2017/10/evernote-snapshot-20171031-164120.png?w=232&h=300 "Evernote Snapshot 20171031 164120")

我们发现, A为右下角点的铅笔画大正方形A全为1需要的条件是:

```
绿色的B, 黑色的C和粉色的D全都为1
```

加上

```
并且A自己的最右下角点为1
```

所以我们只需要在左点, 上点和左上点各自最大正方形的边长取最小值, 再加1就行了. 状态方程变成

```
if matrix[i][j] == 1
    f[i][j] = min(f[i - 1][j], f[i][j-1], f[i-1][j-1]) + 1;
if matrix[i][j] == 0
    f[i][j] = 0
```

### Code

```java
public class Solution {
    /**
     * @param matrix: a matrix of 0 and 1
     * @return: an integer
     */
    public int maxSquare(int[][] matrix) {
        // write your code here
        int ans = 0;
        if (matrix == null || matrix.length == 0 || matrix[0] == null || matrix[0].length == 0) {
            return 0;
        }
        
        int n = matrix.length, m = matrix[0].length;
        int[][] res = new int[n][m];
        for (int i = 0; i < n; i++) {
            res[i][0] = matrix[i][0];
            ans = Math.max(res[i][0], ans);
            for (int j = 1; j < m; j++) {                 
                if (i > 0) {
                    if (matrix[i][j] > 0) {
                        res[i][j] = 1 + Math.min(res[i - 1][j], 
                                                 Math.min(res[i][j - 1], 
                                                          res[i - 1][j - 1]));
                    } else {
                        res[i][j] = 0;
                    }
                } else {
                    res[i][j] = matrix[i][j];
                }
                ans = Math.max(res[i][j], ans);
            }
        }
        return ans*ans;
    }
}
```

### 滚动数组优化 {#滚动数组优化-1}

需要多少个状态, 就存多少个.

求第i个状态, 如果只与i-1有关, 那就只需要两个数组. 用previous数组, 推now数组.  
所以上一个解法中, j可以都模2.

那i为什么不能模呢?  
因为如果i模了的话, 下一行左边开始的时候, 存的还是上一行最右边末尾的值, 不行哒~ 状态方程变为：

```
if matrix[i][j] == 1
    f[i%2][j] = min(f[(i - 1)%2][j], f[i%2][j-1], f[(i-1)%2][j-1]) + 1;
if matrix[i][j] == 0
    f[i%2][j] = 0
```

其中要注意初始化和答案也要记得模：

初始化 Intialization：

```
f[i%2][0] = matrix[i][0];
f[0][j] = matrix[0][j];
```

答案 Answer

```
max{f[i%2][j]}
```

```java
public class Solution {
    /**
     * @param matrix: a matrix of 0 and 1
     * @return: an integer
     */
    public int maxSquare(int[][] matrix) {
        if(matrix==null || matrix.length==0 || matrix[0]==null || matrix[0].length==0) {
            return 0;
        }
        
        int n = matrix.length, m = matrix[0].length;
        int[][] dp = new int[n][m];
        int maxEdge = 0;
        for (int i = 0; i < m; i++) {
            dp[0][i] = matrix[0][i];
            if (matrix[0][i] > maxEdge) {
                maxEdge = matrix[0][i];
            }
        }
        
        for (int i = 1; i < n; i++) {
            dp[i % 2][0] = matrix[i][0];
            for (int j = 1; j < m; j++) {
                if (matrix[i][j] == 1) {
                    dp[i % 2][j] = Math.min(dp[(i - 1) % 2][j - 1], 
                                        Math.min(
                                            dp[i % 2][j - 1],
                                            dp[(i - 1) % 2][j]
                                            )
                                        ) + 1;
                }
                else {
                    dp[i % 2][j] = 0;
                }
                
                if (dp[i % 2][j] > maxEdge) {
                    maxEdge = dp[i % 2][j];
                }
            }
        }
        
        return maxEdge * maxEdge;
        
    }
}
```



