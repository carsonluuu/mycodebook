# [Container With Most Water](http://www.lintcode.com/en/problem/container-with-most-water/)

Givennnon-negative integersa1,a2, ...,an , where each represents a point at coordinate \(i,ai\).nvertical lines are drawn such that the two endpoints of lineiis at \(i,ai\) and \(i, 0\). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

**Note: **You may not slant the container andnis at least 2.



![](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg)

The above vertical lines are represented by array \[1,8,6,2,5,4,8,3,7\]. In this case, the max area of water \(blue section\) the container can contain is 49.

### **Example**

```
Input: [1,8,6,2,5,4,8,3,7]

Output: 49
```

### Note

头尾双指针，移动标准是更低的长度，维护最大面积

### Code

```java
class Solution {
    public int maxArea(int[] height) {
        int l = 0, r = height.length - 1;
        int res = 0;
        while (l < r) {
            res = Math.max(res, Math.min(height[l], height[r])*(r-l));
            if (height[l] < height[r])
                l++;
            else
                r--;
        }
        return res;
    }
}

```



