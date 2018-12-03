# [Most Stones Removed with Same Row or Column](https://leetcode.com/problems/most-stones-removed-with-same-row-or-column/description/)

On a 2D plane, we place stones at some integer coordinate points.  Each coordinate point may have at most one stone.

Now, a _move _consists of removing a stone that shares a column or row with another stone on the grid.

What is the largest possible number of moves we can make?

### Example

**Example 1:**

```
Input: stones = [[0,0],[0,1],[1,0],[1,2],[2,1],[2,2]]
Output: 5
```

**Example 2:**

```
Input: stones = [[0,0],[0,2],[1,1],[2,0],[2,2]]
Output: 3
```

**Example 3:**

```
Input: stones = [[0,0]]
Output: 0
```

### Note

行或者列相等的时候，就union成一个联通块，这个联通块最后最少会剩一个，也是最大的移除操作数目

所以有几个联通块就会剩下几个。结果就是`总石头数减去联通块数目`

暴力并查集

Time: O\(n^2\)

Space: O\(n\)

