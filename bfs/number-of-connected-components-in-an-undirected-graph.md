# Number of Connected Components in an Undirected Graph

Given`n`nodes labeled from`0`to`n - 1`and a list of undirected edges \(each edge is a pair of nodes\), write a function to find the number of connected components in an undirected graph.

### Example

**Example 1:**

```
Input: n = 5 and edges = [[0, 1], [1, 2], [3, 4]]

     0          3
     |          |
     1 --- 2    4 

Output: 
2
```

**Example 2:**

```
Input: n = 5 and edges = [[0, 1], [1, 2], [2, 3], [3, 4]]

     0           4
     |           |
     1 --- 2 --- 3

Output:  
1
```

### Note

类似number of the island（DFS/BFS）

### Code

```java
class Solution {
    public int countComponents(int n, int[][] edges) {
        if (n <= 1) {
            return n;
        }
        Map<Integer, Set<Integer>> graph = initializeGraph(n, edges);

        Set<Integer> visited = new HashSet<>();
        int res = 0;
        for (int node = 0; node < n; node++) {
            if (visited.add(node)) {
                dfs(graph, node, visited);
                res++;
            }
        }

        return res;
    }

    private void dfs(Map<Integer, Set<Integer>> graph, int node, Set<Integer> visited) {
        for (Integer neighbor : graph.get(node)) {
            if (visited.add(neighbor)) {
                dfs(graph, neighbor, visited);
            }
        }
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

```java
class Solution {
    public int countComponents(int n, int[][] edges) {
        if (n <= 1) {
            return n;
        }

        int res = 0;
        Map<Integer, Set<Integer>> graph = initializeGraph(n, edges);
        Set<Integer> visited = new HashSet<>();
        for (int node = 0; node < n; node++) {
            if (visited.add(node)) {
                bfs(graph, node, visited);
                res++;
            }
        }

        return res;
    }

    private void bfs (Map<Integer, Set<Integer>> graph, int node, Set<Integer> set) {
        Queue<Integer> q = new LinkedList<>();
        q.offer(node);
        set.add(node);
        while (!q.isEmpty()) {
            Integer curr = q.poll();
            for (Integer neighbor : graph.get(curr)) {
                if (!set.contains(neighbor)) {
                    q.offer(neighbor);
                    set.add(neighbor);
                }
            }
        }

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



