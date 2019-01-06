# [Minimum Height Trees](https://leetcode.com/problems/minimum-height-trees/description/)

For an undirected graph with tree characteristics, we can choose any node as the root. The result graph is then a rooted tree. Among all possible rooted trees, those with minimum height are called minimum height trees \(MHTs\). Given such a graph, write a function to find all the MHTs and return a list of their root labels.

**Format**  
The graph contains`n`nodes which are labeled from`0`to`n - 1`. You will be given the number`n`and a list of undirected`edges`\(each edge is a pair of labels\).

You can assume that no duplicate edges will appear in`edges`. Since all edges are undirected,`[0, 1]`is the same as`[1, 0]`and thus will not appear together in`edges`.

### Example

**Example 1 :**

```
Input:
n = 4, edges = [[1, 0], [1, 2], [1, 3]]
        0
        |
        1
       / \
      2   3 
Output:
[1]
```

**Example 2 :**

```
Input:
n = 6, edges = [[0, 3], [1, 3], [2, 3], [4, 3], [5, 4]]
     0  1  2
      \ | /
        3
        |
        4
        |
        5 
Output:
[3, 4]
```

### Note



### Code

```java
class Solution {
    public List<Integer> findMinHeightTrees(int n, int[][] edges) {
        List<Integer> res = new ArrayList<>();
        if (n == 1) {
            res.add(0);
            return res;
        }
        
        Map<Integer, Set<Integer>> graph = new HashMap<>();
        for (int i = 0; i < n; i++) {
            graph.put(i, new HashSet<Integer>());
        }
        
        int[] indegree = new int[n];
        for (int i = 0; i < edges.length; i++) {
            int u = edges[i][0];
            int v = edges[i][1];
            graph.get(u).add(v);
            graph.get(v).add(u);
            indegree[u]++;
            indegree[v]++;
        }
        
        Queue<Integer> q = new LinkedList<>();
        for (int i = 0; i < n; i++) {
            if (indegree[i] == 1) {
                q.offer(i);
            }
        }
        
        while (!q.isEmpty()) {
            int size = q.size();
            res = new ArrayList<Integer>();
            for (int i = 0; i < size; i++) {
                Integer leaf = q.poll();
                res.add(leaf);
                indegree[leaf]--;
                for (Integer parent : graph.get(leaf)) {
                    indegree[parent]--;
                    if (indegree[parent] == 1) {
                        q.offer(parent);
                    }
                }
            }
        }

        return res;
    }
}
```



