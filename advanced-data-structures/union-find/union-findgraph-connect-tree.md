# Graph Valid Tree

Given`n`nodes labeled from`0`to`n - 1`and a list of`undirected`edges \(each edge is a pair of nodes\), write a function to check whether these edges make up a valid tree.

### Example

Given`n = 5`and`edges = [[0, 1], [0, 2], [0, 3], [1, 4]]`, return true.

Given`n = 5`and`edges = [[0, 1], [1, 2], [2, 3], [1, 3], [1, 4]]`, return false.

You can assume that no duplicate edges will appear in edges. Since all edges are`undirected`,`[0, 1]`is the same as`[1, 0]`and thus will not appear together in edges.

### Note

给定一个 Set of Nodes ，Tree 要满足两个条件：

* 无环
* 单 root 节点

![](https://mnmunknown.gitbooks.io/algorithm-notes/content/Tree_Definition.PNG)

把这两点搞清楚之后，这题就很简单了。先一个一个 edge 去加，如果发现有环的话直接返回 false；否则跑到最后，看看最终的 number of connected components 是不是 1.

### Code

```java
public class Solution {
    /**
     * @param n: An integer
     * @param edges: a list of undirected edges
     * @return: true if it's a valid tree, or false
     */

    private static class UnionFind {
        int[] father;
        int count;
        public UnionFind(int n) {
            father = new int[n];
            count = n;
            for (int i = 0; i < n; i++) {
                father[i] = i;
            }
        }

        private int find(int x) {
            if (father[x] == x) {
                return father[x];
            }

            return father[x] = find(father[x]);
        }

        private void union(int a, int b) {
            int root_a = find(a);
            int root_b = find(b);
            if (root_a != root_b) {
                father[root_a] = root_b;   
                count--;
            }
        }

        private boolean query(int a, int b) {
            return find(a) == find(b);
        }
    }

    public boolean validTree(int n, int[][] edges) {
        // write your code here
        if (n == 0) {
            return false;
        }

        if (edges.length != n - 1) {
            return false;
        }

        UnionFind uf = new UnionFind(n);

        for (int[] edge : edges) {
            //
            // if (uf.query(edge[0], edge[1])) {
            //     return false;
            // }

            uf.union(edge[0], edge[1]);
        }

        return uf.count == 1;
    }
}
```



