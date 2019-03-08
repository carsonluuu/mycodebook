# [Max Points on a Line](https://leetcode.com/problems/max-points-on-a-line/description/)

Given _n _points on a 2D plane, find the maximum number of points that lie on the same straight line.

### **Example**

**Example 1:**

```
Input:
 [[1,1],[2,2],[3,3]]

Output:
 3

Explanation:

^
|
|        o
|     o
|  o  
+------------->
0  1  2  3  4
```

**Example 2:**

```
Input:
 [[1,1],[3,2],[5,3],[4,1],[2,3],[1,4]]

Output:
 4

Explanation:
^
|
|  o
|     o        o
|        o
|  o        o
+------------------->
0  1  2  3  4  5  6
```

### Note

### Code

```java
/**
 * Definition for a point.
 * class Point {
 *     int x;
 *     int y;
 *     Point() { x = 0; y = 0; }
 *     Point(int a, int b) { x = a; y = b; }
 * }
 */
class Solution {
    public int maxPoints(Point[] points) {
        if (points == null || points.length == 0) return 0;
        int res = 0, len = points.length;
        Map<String, Integer> map = new HashMap<>();
        for (int i = 0; i < len; i++) {
            int overlap = 0, max = 0;
            map.clear();
            for (int j = i + 1; j < len; j++) {
                int x = points[j].x - points[i].x;
                int y = points[j].y - points[i].y;
                if (x == 0 && y == 0) {
                    overlap++;
                    continue;
                }
                int gcd = findGCD(x, y);
                if (gcd != 0) {
                    x /= gcd;
                    y /= gcd;
                }
                String key = x + "@" + y;
                map.put(key, map.getOrDefault(key, 0) + 1);
                max = Math.max(max, map.get(key));
            }
            res = Math.max(res, max + overlap + 1);
        }
        return res;
    }
    
    private int findGCD(int a, int b) {
        if (b == 0) {
            return a;
        }
        return findGCD(b, a % b);
    }
}
```



