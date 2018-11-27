# Search a 2D Matrix

Write an efficient algorithm that searches for a value in an_m_x_n_matrix.

This matrix has the following properties:

* Integers in each row are sorted from left to right.
* The first integer of each row is greater than the last integer of the previous row.

### Example

Consider the following matrix:

```
[
    [1, 3, 5, 7],
    [10, 11, 16, 20],
    [23, 30, 34, 50]
]
```

Given`target = 3`, return`true`

### Note

降维，[矩阵转化为数组](/appendix/3math/matrix-coordinate.md)

### Code

```java
public class Solution {
    /**
     * @param matrix: matrix, a list of lists of integers
     * @param target: An integer
     * @return: a boolean, indicate whether matrix contains target
     */
    public boolean searchMatrix(int[][] matrix, int target) {
        if (matrix == null || matrix.length == 0) {
            return false;
        }
        
        if (matrix[0] == null || matrix[0].length == 0) {
            return false;
        }
        int row = matrix.length;
        int col = matrix[0].length;
        int start = 0, end = row * col - 1;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            int number = matrix[mid / col][mid % col];
            if (number == target) {
                return true;
            } else if (number < target) {
                start = mid;
            } else {
                end = mid;
            }
        }
        
        if (matrix[start / col][start % col] == target ||
            matrix[end / col][end % col] == target) {
            return true;
        }
        return false;
    }
}
```



