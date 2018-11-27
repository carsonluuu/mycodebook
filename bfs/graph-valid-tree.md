# Graph Valid Tree

Given`n`nodes labeled from`0`to`n-1`and a list of undirected edges \(each edge is a pair of nodes\), write a function to check whether these edges make up a valid tree.

```
you can assume that no duplicate edges will appear in edges. 
Since all edges are undirected, [0,1] is the same as [1,0] and thus will not appear together in edges.
```

### Example

**Example 1:**

```
Input:n = 5, and edges = [[0,1], [0,2], [0,3], [1,4]]
Output: true
```

**Example 2:**

```
Input:n = 5, and edges = [[0,1], [1,2], [2,3], [1,3], [1,4]]
Output: false
```

### Code1

**DFS**

make sure there's no cycle：记录parent，对于visited过的节点，有环的话会有neighbor的值不等于其parent，因为有环又会dfs回来，相反的没有环的话，visited的neighbor都会等于其parent，因为这里是无向图。但是这里假设没有自己点成环的情况，如\[1,1\]

make sure all vertices are connected： 利用visited数组，对于树不能有不连接的部分

```java
class Solution {
    public boolean validTree(int n, int[][] edges) {
        if (n == 0) {
            return false;
        }

        /**
        if (edges.length != n - 1) {
            return false;
        }
        **/

        Map<Integer, Set<Integer>> graph = initializeGraph(n, edges);

        boolean[] visited = new boolean[n];

        // make sure there's no cycle
        if (hasCycle(graph, 0, visited, -1)) {
            return false;
        }

        // make sure all vertices are connected
        for (int i = 0; i < n; i++) {
            if (!visited[i]) {
                return false;
            }
        }

        return true;
    }

    private boolean hasCycle(Map<Integer, Set<Integer>> graph, 
                             int node, boolean[] visited, int parent) {
        visited[node] = true;

        for (Integer neighbor : graph.get(node)) {
            // If an adjacent is not visited, then recur for that adjacent
            if (!visited[neighbor]) {
                if (hasCycle(graph, neighbor, visited, node)) {
                    return true;
                }
            } else if (neighbor != parent) {
                // If an adjacent is visited and not parent of current vertex, then there is a cycle.
                return true;
            }
        }

        return false;
    }

    private Map<Integer, Set<Integer>> initializeGraph(int n, int[][] edges) {
        Map<Integer, Set<Integer>> graph = new HashMap<>();
        for (int i = 0; i < n; i++) {
            graph.put(i, new HashSet<Integer>());
        }

        for (int i = 0; i < edges.length; i++) {
            int u = edges[i][0];
            int v = edges[i][1];
            graph.get(u).add(v);
            graph.get(v).add(u);
        }

        return graph;
    }
}
```

### Code2

两个条件判断是否为树：（1）无环（2）连通。首先判断无环：如果是树的话，两个点之间有且只有一条path，所以如果有`n`个点，那么一定有且只有`n-1`条边。然后用BFS判断是否连通，如果连通，访问到的点的数量一定等于`n`。

```java
public class Solution {
    /**
     * @param n an integer
     * @param edges a list of undirected edges
     * @return true if it's a valid tree, or false
     */
    public boolean validTree(int n, int[][] edges) {
        if (n == 0) {
            return false;
        }

        if (edges.length != n - 1) {
            return false;
        }

        Map<Integer, Set<Integer>> graph = initializeGraph(n, edges);

        // bfs
        Queue<Integer> queue = new LinkedList<>();
        Set<Integer> hash = new HashSet<>();

        queue.offer(0);
        hash.add(0);
        while (!queue.isEmpty()) {
            int node = queue.poll();
            for (Integer neighbor : graph.get(node)) {
                if (！hash.contains(neighbor)) {
                    hash.add(neighbor);
                    queue.offer(neighbor);
                }
            }
        }

        return (hash.size() == n);
    }

    private Map<Integer, Set<Integer>> initializeGraph(int n, int[][] edges) {
        Map<Integer, Set<Integer>> graph = new HashMap<>();
        for (int i = 0; i < n; i++) {
            graph.put(i, new HashSet<Integer>());
        }

        for (int i = 0; i < edges.length; i++) {
            int u = edges[i][0];
            int v = edges[i][1];
            graph.get(u).add(v);
            graph.get(v).add(u);
        }

        return graph;
    }
}
```



