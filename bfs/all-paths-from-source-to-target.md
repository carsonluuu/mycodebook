# All Paths From Source to Target

Given a directed, acyclic graph of`N`nodes.  Find all possible paths from node`0`to node`N-1`, and return them in any order.

The graph is given as follows:  the nodes are 0, 1, ..., graph.length - 1.  graph\[i\] is a list of all nodes j for which the edge \(i, j\) exists.

```
- The number of nodes in the graph will be in the range [2, 15].
- You can print different paths in any order, but you should keep the order of nodes inside one path.
```

### Example

```
Example:
Input: [[1,2], [3], [3], []] 
Output: [[0,1,3],[0,2,3]] 
Explanation: The graph looks like this:
0--->1
|    |
v    v
2--->3
There are two paths: 0 -> 1 -> 3 and 0 -> 2 -> 3.
```

### Code

```java
class Solution {
    public List<List<Integer>> allPathsSourceTarget(int[][] graph) {
        List<List<Integer>> res = new ArrayList<>();
        List<Integer> path = new ArrayList<>();
        boolean[] isVisited = new boolean[graph.length];
        path.add(0);
        helper(0, graph.length - 1, graph, isVisited, path, res);
        return res;
    }

    private void helper(Integer u, Integer d, 
                        int[][] graph, boolean[] isVisited,
                        List<Integer> path,
                        List<List<Integer>> res) {
        if (u.equals(d)) {
            res.add(new ArrayList<>(path));
        }

        isVisited[u] = true;
        for (Integer i : graph[u]) {
            if (!isVisited[i]) {
                // store current node in path[]
                path.add(i);
                helper(i, graph.length - 1, graph, isVisited, path, res);                
                // remove current node in path[]
                path.remove(i);
            }
        }
        // Mark the current node
        isVisited[u] = false;
    }
}
```

```java
class Solution {
    public List<List<Integer>> allPathsSourceTarget(int[][] graph) {
        List<List<Integer>> res = new ArrayList<>();
        List<Integer> path = new ArrayList<>();

        path.add(0);
        dfsSearch(graph, 0, res, path);

        return res;
    }

    private void dfsSearch(int[][] graph, int node, List<List<Integer>> res, List<Integer> path) {
        if (node == graph.length - 1) {
            res.add(new ArrayList<Integer>(path));
            return;
        }

        for (int nextNode : graph[node]) {
            path.add(nextNode);
            dfsSearch(graph, nextNode, res, path);
            path.remove(path.size() - 1);
        }
    }
}
```



