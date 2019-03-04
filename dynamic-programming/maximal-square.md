# Maximal Square

Given a 2D binary matrix filled with 0's and 1's, find the largest square containing all 1's and return its area.

### Example

**Example 1:**

```
Input:
[
  [1, 0, 1, 0, 0],
  [1, 0, 1, 1, 1],
  [1, 1, 1, 1, 1],
  [1, 0, 0, 1, 0]
]
Output: 4

```

**Example 2:**

```
Input:
[
  [0, 0, 0],
  [1, 1, 1]
]
Output: 1

```

### Note

```
res[i][j] = 1 + Math.min(res[i-1][j],Math.min(res[i][j-1],res[i-1][j-1]));
```

i=0和j=0 初始为矩阵值

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
        if (matrix == null || matrix.length == 0 || 
            matrix[0] == null || matrix[0].length == 0) {
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
                        res[i][j] = 1 + Math.min(res[i-1][j],
                                                Math.min(res[i][j-1],
                                                         res[i-1][j-1]));
                    } else {
                        res[i][j] = 0;
                    }
                } else {
                    res[i][j] = matrix[i][j];
                }
                ans = Math.max(res[i][j], ans);
            }
        }
        return ans * ans;
    }
}

```



