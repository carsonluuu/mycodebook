# Is Graph Bipartite

Given an undirected `graph`, return`true`if and only if it is bipartite.

Recall that a graph is\_bipartite\_if we can split it's set of nodes into two independent subsets A and B such that every edge in the graph has one node in A and another node in B.

The graph is given in the following form:`graph[i]`is a list of indexes`j`for which the edge between nodes`i`and`j`exists.  Each node is an integer between`0`and`graph.length - 1`.  There are no self edges or parallel edges:`graph[i]`does not contain`i`, and it doesn't contain any element twice.

```
1.graph will have length in range [1, 100].
2.graph[i] will contain integers in range [0, graph.length - 1].
3.graph[i] will not contain i or duplicate values.
4.The graph is undirected: if any element j is in graph[i], then i will be in graph[j].
```

### Example

```
Input:
 [[1,3], [0,2], [1,3], [0,2]]

Output:
 true

Explanation:

The graph looks like this:
0----1
|    |
|    |
3----2
We can divide the vertices into two groups: {0, 2} and {1, 3}.
```

```
Input:
 [[1,2,3], [0,2], [0,1,3], [0,2]]

Output:
 false

Explanation:

The graph looks like this:
0----1
| \  |
|  \ |
3----2
We cannot find a way to divide the set of nodes into two independent subsets.
```

### Note

1. Assign RED color to the source vertex \(putting into set U\).  
2. Color all the neighbors with BLUE color \(putting into set V\).  
3. Color all neighbor’s neighbor with RED color \(putting into set U\).  
4. This way, assign color to all vertices such that it satisfies all the constraints of m way coloring problem where m = 2.  
5. While assigning colors, **if we find a neighbor which is colored with same color as current vertex**, then the graph cannot be colored with 2 vertices \(or graph is not Bipartite\)

### Code

```java
class Solution {
    public boolean isBipartite(int[][] graph) {
        if (graph == null || graph.length == 0) return false;
        int[] color = new int[graph.length];
        Queue<Integer> q = new LinkedList<>();
        //Divide the node in two sets such that no two nodes in same set are linked
        //[[1,2,3], [0,2], [0,1,3], [0,2]]
        for (int i = 0; i < graph.length; i++) {
            if (color[i] == 0) {
                //color and send in queue
                q.offer(i);
                color[i] = 1;
                while (!q.isEmpty()) {
                    int node = q.poll();
                    for (int child : graph[node]) {
                        if (color[child] == 0) {
                            //color distinct color
                            if (color[node] == 2) color[child] = 1;
                            else color[child] = 2;
                            q.offer(child);
                        } else if (color[child] == color[node]) {
                            return false;
                        }                  
                    }
                }
            }
        }
        return true;
    }
}
```



