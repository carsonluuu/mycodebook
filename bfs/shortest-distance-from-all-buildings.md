# [Shortest Distance from All Buildings](https://leetcode.com/problems/shortest-distance-from-all-buildings/description/)

You want to build a house on anemptyland which reaches all buildings in the shortest amount of distance. You can only move up, down, left and right. You are given a 2D grid of values **0**,**1 **or **2**, where:

* Each **0 **marks an empty land which you can pass by freely.
* Each **1 **marks a building which you cannot pass through.
* Each **2 **marks an obstacle which you cannot pass through.

**Note:**

There will be at least one building. If it is not possible to build such house according to the above rules, return -1.

### Example

```
Input: [[1,0,2,0,1],[0,0,0,0,0],[0,0,1,0,0]]

1 - 0 - 2 - 0 - 1
|   |   |   |   |
0 - 0 - 0 - 0 - 0
|   |   |   |   |
0 - 0 - 1 - 0 - 0

Output: 7 

Explanation: Given three buildings at (0,0), (0,4), (2,2), and an obstacle at (0,2),
             the point (1,2) is an ideal empty land to build a house, as the total 
             travel distance of 3+3+1=7 is minimal. So return 7.
```

### Note

O\(m^2\*n^2\)的BFS做法

对于每个空地做一下BFS，然后算到各个建筑最近距离和；然后找出最小的那个空地

### Code

```

```



