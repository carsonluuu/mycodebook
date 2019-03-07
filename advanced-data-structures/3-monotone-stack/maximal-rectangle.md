# [Maximal Rectangle](https://leetcode.com/problems/maximal-rectangle/)

Given a 2D binary matrix filled with 0's and 1's, find the largest rectangle containing only 1's and return its area.

### **Example**

```
Input:
[
  ["1","0","1","0","0"],
  ["1","0","1","1","1"],
  ["1","1","1","1","1"],
  ["1","0","0","1","0"]
]
Output: 6
```

### Note

之前题目的2D版本

对于test case：

降维，记录1D行的最大矩形大小

```
  ["1","0","1","0","0"] --> 0
  ["2","0","2","1","1"] --> 3*1
  ["3","1","3","2","2"] --> 3*2
  ["4","1","3","3","2"] --> 5*1
```

多开一个空间来使最末端能pop：`int[] height = new int[n + 1]` 

### Code

```java
class Solution {
    public int maximalRectangle(char[][] matrix) {
        int res = 0; 
        if (matrix == null || matrix.length == 0 ||
            matrix[0] == null || matrix[0].length == 0) {
            return res;
        }
        
        int m = matrix.length;
        int n = matrix[0].length;
        int[] height = new int[n + 1];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (matrix[i][j] == '1') {
                    height[j] += 1;
                } else {
                    height[j] = 0;
                }
            }
            
            res = Math.max(res, hist(height));
        }
        
        return res;
    }
    
    public int hist(int[] height) {
        int res = 0;
        Stack<Integer> stack = new Stack<>();
        for (int i = 0; i < height.length; i++) {
            while (!stack.isEmpty() && height[i] <= height[stack.peek()]) {
                int h = height[stack.pop()];
                int w = stack.isEmpty() ? i : i - stack.peek() - 1;
                res = Math.max(res, h * w);
            }
            stack.push(i);
        }
        
        return res;
    }
}
```



