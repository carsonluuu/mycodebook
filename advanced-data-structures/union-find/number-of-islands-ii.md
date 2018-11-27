# Number of Islands II

Given a n,m which means the row and column of the 2D matrix and an array of pair A\( size k\). Originally, the 2D matrix is all 0 which means there is only sea in the matrix. The list pair has k operator and each operator has two integer A\[i\].x, A\[i\].y means that you can change the grid matrix\[A\[i\].x\]\[A\[i\].y\] from sea to island. Return how many island are there in the matrix after each operator.

**Note**: 0 is represented as the sea, 1 is represented as the island. If two 1 is adjacent, we consider them in the same island. We only consider up/down/left/right adjacent.

### Example

Given`n`=`3`,`m`=`3`, array of pair A =`[(0,0),(0,1),(2,2),(2,1)]`.

return`[1,1,2,2]`.

### Note

在线算法！

Union-Find初始化grid废掉了M\*N的时间

剩下的就是扩展+联通

注意count的累加：新点进来加一，相邻联通减一。因为点是一个一个进来的

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

public class Solution {
    /**
     * @param n: An integer
     * @param m: An integer
     * @param operators: an array of point
     * @return: an integer array
     */
    private static class UnionFind {
        int[] father;
        public UnionFind(int n) {
            father = new int[n];
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
            int root_a = find(a);
            int root_b = find(b);
            father[root_a] = root_b;
        }
    }
    public List<Integer> numIslands2(int m, int n, Point[] operators) {
        // write your code here
        UnionFind uf = new UnionFind(m * n);
        int[][] grids = new int[m][n];
        int[] dx = {0, -1, 0, 1};
        int[] dy = {1, 0, -1, 0};

        List<Integer> ans = new ArrayList<>();
        int count = 0;
        if (operators == null || operators.length == 0) {
            return ans;
        }

        for (Point op : operators) {
            int x = op.x;
            int y = op.y;
            if (grids[x][y] != 1) {
                count++;
                grids[x][y] = 1;
                int id = converttoId(x, y, n);
                for (int i = 0; i < 4; i++) {
                    int nx = x + dx[i];
                    int ny = y + dy[i];
                    if (0 <= nx && nx < m && 
                        0 <= ny && ny < n && grids[nx][ny] == 1) {

                        int nid = converttoId(nx, ny, n);

                        int fa = uf.find(id);
                        int nfa = uf.find(nid);
                        if (fa != nfa) {
                            count--;
                            uf.union(id, nid);
                        }
                    }
                }
            }

            ans.add(count);
        }

        return ans;
    }

    private int converttoId(int x, int y, int m){
        return x * m + y;
    }

}
```



