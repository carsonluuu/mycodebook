# Smallest Rectangle Enclosing Black Pixels

An image is represented by a binary matrix with`0`as a white pixel and`1`as a black pixel. The black pixels are connected, i.e., there is only one black region. Pixels are connected horizontally and vertically. Given the location`(x, y)`of one of the black pixels, return the area of the smallest \(axis-aligned\) rectangle that encloses all black pixels.

### Example

For example, given the following image:

```
[
  "0010",
  "0110",
  "0100"
]
```

and x =`0`, y =`2`,  
Return`6`.

### Note

![](/assets/rectEnclosing.png)

即找出黑色虚线虚线框

黑色虚线框是什么呢,  是上下左右四个位置:

左:第一个出现绿色的列 \(0 to y\)

右:最后一个出现绿色的列 \(y to n - 1\)

上:第一个绿的行 \(0 to x\)

下:最后一个绿的行 \(x to m - 1\)

二分法的判断条件是该**行**或者**列**是不是全部都是0

### Code

```java
public class Solution {
    /**
     * @param image: a binary matrix with '0' and '1'
     * @param x: the location of one of the black pixels
     * @param y: the location of one of the black pixels
     * @return: an integer
     */
    private int m, n;
    public int minArea(char[][] image, int x, int y) {
        // write your code here
        m = image.length;
        n = image[0].length;
        
        int left = findLeft(image, 0, y);
        int right = findRight(image, y, n - 1);
        int top = findTop(image, 0, x);
        int bottom = findBottom(image, x, m - 1);
        
        return (right - left + 1) * (bottom - top + 1);
    }
    
    private int findLeft(char[][] image, int start, int end) {
        while (start + 1 < end) {
            int mid = (end - start) / 2 + start;
            if (isColEmpty(image, mid)) {
                start = mid;
            } else {
                end = mid;
            }
        }   
        
        if (!isColEmpty(image, start)) {
            return start;
        }
        return end;
    }

    private int findRight(char[][] image, int start, int end) {
        while (start + 1 < end) {
            int mid = (end - start) / 2 + start;
            if (isColEmpty(image, mid)) {
                end = mid;
            } else {
                start = mid;
            }
        }   
        
        if (!isColEmpty(image, end)) {
            return end;
        }
        return start;
    }
    
    private int findTop(char[][] image, int start, int end) {
        while (start + 1 < end) {
            int mid = (end - start) / 2 + start;
            if (isRowEmpty(image, mid)) {
                start = mid;
            } else {
                end = mid;
            }
        }   
        
        if (!isRowEmpty(image, start)) {
            return start;
        }
        return end;
    }
    
    private int findBottom(char[][] image, int start, int end) {
        while (start + 1 < end) {
            int mid = (end - start) / 2 + start;
            if (isRowEmpty(image, mid)) {
                end = mid;
            } else {
                start = mid;
            }
        }   
        
        if (!isRowEmpty(image, end)) {
            return end;
        }
        return start;
    }
    
    private boolean isRowEmpty(char[][] image, int row) {
        for (int j = 0; j < n; j++) {
            if (image[row][j] == '1') {
                return false;
            }
        }
        return true;
    }
    
    private boolean isColEmpty(char[][] image, int col) {
        for (int i = 0; i < m; i++) {
            if (image[i][col] == '1') {
                return false;
            } 
        }
        
        return true;
    }
}
```





