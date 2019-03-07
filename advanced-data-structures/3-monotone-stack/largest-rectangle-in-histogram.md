# [Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/)

Given \_n \_non-negative integers representing the histogram's bar height where the width of each bar is 1, find the area of largest rectangle in the histogram.

![](https://assets.leetcode.com/uploads/2018/10/12/histogram.png)  
Above is a histogram where width of each bar is 1, given height =`[2,1,5,6,2,3]`.

![](https://assets.leetcode.com/uploads/2018/10/12/histogram_area.png)  
The largest rectangle is shown in the shaded area, which has area =`10`unit.

### **Example**

```
Input:
 [2,1,5,6,2,3]

Output:
 10
```

### Note

单调栈严格递增栈，可以跑一下test case：

| height | 2 | 6 | 5 | 3 | 2 | 1 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **width** | 1 | 1=4-2-1 | 2=4-1-1 | 1=6-4-1 | 4=6-1-1 | 6 |
| **i** | 1 | 4 | 4 | 6 | 6 | 6 |
| **s.peek\(\)** | null | 2 | 1 | 4 | 1 | null |
| **res** | 2 | 6 | 10 | 3 | 8 | 6 |

### Code

```java
class Solution {
    public int largestRectangleArea(int[] heights) {
        int res = 0;
        if (heights == null || heights.length == 0) {
            return res;
        }

        Stack<Integer> stack = new Stack<Integer>();    
        for (int i = 0; i <= heights.length; i++) {
            int h = (i == heights.length) ? -1 : heights[i];

            while (!stack.isEmpty() && h <= heights[stack.peek()]) {
                int height = heights[stack.pop()];
                int w = stack.isEmpty() ? i : i - stack.peek() - 1;
                System.out.println(height * w);
                res = Math.max(res, height * w);
            }
            stack.push(i);
        }

        return res; 
    }
}
```



