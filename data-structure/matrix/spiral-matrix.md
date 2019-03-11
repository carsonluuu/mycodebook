# [Spiral Matrix](https://leetcode.com/problems/spiral-matrix/description/)

Given a matrix of_m_x_n_elements \(_m _rows, _n _columns\), return all elements of the matrix in spiral order.

### Example

**Example 1:**

```
Input:

[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]

Output:
 [1,2,3,6,9,8,7,4,5]

```

**Example 2:**

```
Input:

[
  [1, 2, 3, 4],
  [5, 6, 7, 8],
  [9,10,11,12]
]

Output:
 [1,2,3,4,8,12,11,10,9,5,6,7]
```

### Note

利用方向数组进行遍历

### Code

```java
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        List<Integer> res = new ArrayList<>();
        if(matrix == null || matrix.length == 0) return res;
        int R = matrix.length, C = matrix[0].length;
        int[] dr = {0, 1, 0, -1};
        int[] dc = {1, 0, -1, 0};
        boolean[][] seen = new boolean[R][C];
        int r = 0, c = 0, di = 0;
        for(int i = 0; i < R*C; i++){
            res.add(matrix[r][c]);
            seen[r][c] = true;
            int rNext = r + dr[di];
            int cNext = c + dc[di];
            if(rNext >= 0 && rNext < R && cNext >= 0 && cNext < C && !seen[rNext][cNext]){                
                r = rNext;
                c = cNext;
            }else{
                di = (di + 1)%4;
                r += dr[di];
                c += dc[di];                
            }
                
        }
        return res;
    }
}
```



