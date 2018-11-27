# [Diagonal Traverse](https://leetcode.com/problems/diagonal-traverse/description/)

Given a matrix of M x N elements \(M rows, N columns\), return all elements of the matrix in diagonal order as shown in the below image.

**Example:**

```
Input:

[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]


Output:  [1,2,4,7,5,3,6,8,9]
```

![](/assets/matrixDiagonalTraverse.png)

### Note

`int[][] dirs = {{-1, 1}, {1, -1}}`表示右上和左下

在出界的时候进行判断：

如果上边出界：行数置为0，反向

如果左边出界：列数置为0，反向

如果下边出界：列数减2，反向

如果右边出界：行数减2，反向

### Code

```
class Solution {
    public int[] findDiagonalOrder(int[][] matrix) {
        if (matrix == null || matrix.length == 0) return new int[0];
        int m = matrix.length, n = matrix[0].length;

        int[] res = new int[m * n];
        int row = 0, col = 0, d = 0;
        int[][] dirs = {{-1, 1}, {1, -1}};

        for (int i = 0; i < m * n; i++) {
            res[i] = matrix[row][col];
            row += dirs[d][0];
            col += dirs[d][1];

            if (row >= m) { row = m - 1; col += 2; d = 1 - d;}
            if (col >= n) { col = n - 1; row += 2; d = 1 - d;}
            if (row < 0)  { row = 0; d = 1 - d;}
            if (col < 0)  { col = 0; d = 1 - d;}
        }

        return res;
    }
}
```



