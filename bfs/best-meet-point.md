# [Best Meeting Point](https://leetcode.com/problems/best-meeting-point/description/)

A group of two or more people wants to meet and minimize the total travel distance. You are given a 2D grid of values 0 or 1, where each 1 marks the home of someone in the group. The distance is calculated using[Manhattan Distance](http://en.wikipedia.org/wiki/Taxicab_geometry), where distance\(p1, p2\) =`|p2.x - p1.x| + |p2.y - p1.y|`.

### **Example**

```
Input:

1 - 0 - 0 - 0 - 1
|   |   |   |   |
0 - 0 - 0 - 0 - 0
|   |   |   |   |
0 - 0 - 1 - 0 - 0


Output: 6 

Explanation: 
Given three people living at 
(0,0), (0,4), and (2,2):

The point (0,2) is an ideal meeting point, as the total travel distance of 2+2+2=6 is minimal. So return 6.
```

### Note

和到各个建筑最短距离不同，不需要暴力去遍历。这里任何点都可以是目标点，也不会有到达不了的情况

1D的话就是[中位数](https://leetcode.com/problems/best-meeting-point/solution/)作为目标点，2D就分别收集row和col，这样都会是排序的，取中位数，算两次距离，相加就是答案

**Complexity analysis**

* Time complexity: O\(mn\)

* Space complexity: O\(mn\)

### Code

```java
public int minTotalDistance(int[][] grid) {
    List<Integer> rows = collectRows(grid);
    List<Integer> cols = collectCols(grid);
    int row = rows.get(rows.size() / 2);
    int col = cols.get(cols.size() / 2);
    return minDistance1D(rows, row) + minDistance1D(cols, col);
}

private int minDistance1D(List<Integer> points, int origin) {
    int distance = 0;
    for (int point : points) {
        distance += Math.abs(point - origin);
    }
    return distance;
}

private List<Integer> collectRows(int[][] grid) {
    List<Integer> rows = new ArrayList<>();
    for (int row = 0; row < grid.length; row++) {
        for (int col = 0; col < grid[0].length; col++) {
            if (grid[row][col] == 1) {
                rows.add(row);
            }
        }
    }
    return rows;
}

private List<Integer> collectCols(int[][] grid) {
    List<Integer> cols = new ArrayList<>();
    for (int col = 0; col < grid[0].length; col++) {
        for (int row = 0; row < grid.length; row++) {
            if (grid[row][col] == 1) {
                cols.add(col);
            }
        }
    }
    return cols;
}
```

更elegant的写法

```
public int minTotalDistance(int[][] grid) {
    List<Integer> rows = collectRows(grid);
    List<Integer> cols = collectCols(grid);
    return minDistance1D(rows) + minDistance1D(cols);
}

private int minDistance1D(List<Integer> points) {
    int distance = 0;
    int i = 0;
    int j = points.size() - 1;
    while (i < j) {
        distance += points.get(j) - points.get(i);
        i++;
        j--;
    }
    return distance;
}
```



