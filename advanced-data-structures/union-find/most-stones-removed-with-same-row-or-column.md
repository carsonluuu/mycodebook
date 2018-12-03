# [Most Stones Removed with Same Row or Column](https://leetcode.com/problems/most-stones-removed-with-same-row-or-column/description/)

On a 2D plane, we place stones at some integer coordinate points.  Each coordinate point may have at most one stone.

Now, a \_move \_consists of removing a stone that shares a column or row with another stone on the grid.

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

Time: O\(n^2\) -&gt; ~O\(n\) or O\(nlogn\)

Space: O\(n\)

### Code

```java
class Solution {
    private static class UnionFind {
        private int[] father;
        private int count;
        public UnionFind(int n) {
            father = new int[n];
            count = n;
            for (int i = 0; i < n; i++) {
                father[i] = i;
            }
        } 
        
        private int find(int x) {
            if (father[x] == x) {
                return x;
            }
            
            return father[x] = find(father[x]);
        }
        
        private void union(int a, int b) {
            int rootA = find(a);
            int rootB = find(b);
            if (rootA != rootB) {
                count--;
                father[rootA] = rootB;
            }
        }
        
        private int query() {
            // write your code here
            return count;
        }
    }
    
    public int removeStones(int[][] stones) {
        int n = stones.length;
        UnionFind uf = new UnionFind(n);
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                if (stones[i][0] == stones[j][0] || 
                    stones[i][1] == stones[j][1]) {
                    uf.union(i, j);
                }
            }
        }
        
        return n - uf.query();
    }
}
```

```java
class Solution {
    public int removeStones(int[][] stones) {
        int N = stones.length;
        DSU dsu = new DSU(20000);

        for (int[] stone: stones)
            dsu.union(stone[0], stone[1] + 10000);

        Set<Integer> seen = new HashSet();
        for (int[] stone: stones)
            seen.add(dsu.find(stone[0]));

        return N - seen.size();
    }
}

class DSU {
    int[] parent;
    public DSU(int N) {
        parent = new int[N];
        for (int i = 0; i < N; ++i)
            parent[i] = i;
    }
    public int find(int x) {
        if (parent[x] != x) parent[x] = find(parent[x]);
        return parent[x];
    }
    public void union(int x, int y) {
        parent[find(x)] = find(y);
    }
}
```



