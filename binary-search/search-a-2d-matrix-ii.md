# Search a 2D Matrix II

Write an efficient algorithm that searches for a value in an m x n matrix, return the occurrence of it.

This matrix has the following properties:

* Integers in each row are sorted from left to right.
* Integers in each column are sorted from up to bottom.
* No duplicate integers in each row or column.

### Example

Consider the following matrix:

```
[
  [1, 3, 5, 7],
  [2, 4, 7, 8],
  [3, 5, 9, 10]
]
```

Given target =`3`, return`2`.

### Note

类似二分逼近的思想

![](/assets/searchInMatrix.png)

橙色线上，从左往右，后一个一定大于前一个；

蓝色线上，后一个可能和前一个相等；

所以左下到右上这条线上呢，相当于中间的位置mid，跟它比较找结果。

**左下角找到右上角**

### Code

```java
public class Solution {
    /**
     * @param matrix: A list of lists of integers
     * @param target: An integer you want to search in matrix
     * @return: An integer indicate the total occurrence of target in the given matrix
     */
    public int searchMatrix(int[][] matrix, int target) {
        // write your code here
        if (matrix == null || matrix.length == 0 
            || matrix[0] == null || matrix[0].length == 0) {
                return 0;
        }
        
        int m = matrix.length;
        int n = matrix[0].length;
        int res = 0;
        int x = m - 1;
        int y = 0;
        while (x >= 0 && y < n) {
            if (matrix[x][y] < target) {
                y++;
            } else if (matrix[x][y] > target) {
                x--;
            } else {
                res++;
                x--;
                y++;
            }
        }
        
        return res;
    }
}
```



