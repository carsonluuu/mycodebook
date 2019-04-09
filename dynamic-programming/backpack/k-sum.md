# [k Sum](https://www.lintcode.com/problem/k-sum/description?_from=ladder&&fromId=4)

Given _n _distinct positive integers, integer _k_\(_k_&lt;=_n_\) and a number _target_.

Find _k _numbers where sum is target. Calculate how many solutions there are?

### Example

**Example 1**

```
Input:
List = [1,2,3,4]
k = 2
target = 5
Output: 2
Explanation: 1 + 4 = 2 + 3 = 5
```

**Example 2**

```
Input:
List = [1,2,3,4,5]
k = 3
target = 6
Output: 1
Explanation: There is only one method. 1 + 2 + 3 = 6
```

### Note

用dp\[i\]\[j\]\[k\]表示前i个数里选j个和为k的方案数

### Code

```
public class Solution {
    /**
     * @param A: An integer array
     * @param k: A positive integer (k <= length(A))
     * @param target: An integer
     * @return: An integer
     */
    public int kSum(int A[], int k, int target) {
        int n = A.length;
        // 用dp[i][j][k]表示前i个数里选j个和为k的方案数
        int[][][] f = new int[n + 1][k + 1][target + 1];
        for (int i = 0; i < n + 1; i++) {
            f[i][0][0] = 1;
        }
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= k && j <= i; j++) {
                for (int t = 1; t <= target; t++) {
                    f[i][j][t] = 0;
                    if (t >= A[i - 1]) {
                        f[i][j][t] = f[i - 1][j - 1][t - A[i - 1]];
                    }
                    f[i][j][t] += f[i - 1][j][t];
                } // for t
            } // for j
        } // for i
        return f[n][k][target];
    }
}
```



