# Detect Cycle in a Directed Graph

Given a directed graph, check whether the graph contains a cycle or not. Your function should return true if the given graph contains at least one cycle, else return false.For example, the following graph contains three cycles 0-&gt;2-&gt;0, 0-&gt;1-&gt;2-&gt;0 and 3-&gt;3, so your function must return true.

### Note

Depth First Traversal can be used to detect a cycle in a Graph. DFS for a connected graph produces a tree. There is a cycle in a graph only if there is a [back edge](http://en.wikipedia.org/wiki/Depth-first_search#Output_of_a_depth-first_search) present in the graph. A back edge is an edge that is from a node to itself \(self-loop\) or one of its ancestor in the tree produced by DFS. In the following graph, there are 3 back edges, marked with a cross sign. We can observe that these 3 back edges indicate 3 cycles present in the graph.

[![](https://cdncontribute.geeksforgeeks.org/wp-content/uploads/cycle.png)](https://cdncontribute.geeksforgeeks.org/wp-content/uploads/cycle.png)

For a disconnected graph, we get the DFS forest as output. To detect cycle, we can check for a cycle in individual trees by checking back edges.

To detect a back edge, we can keep track of vertices currently in recursion stack of function for DFS traversal. **If we reach a vertex that is already in the recursion stack**, then there is a cycle in. The edge that connects current vertex to the vertex in the recursion stack is a back edge. We have used recStack\[\] array to keep track of vertices in the recursion stack.

### Code

```java
class Graph {
    private final int V;
    private final List<List<Integer>> adj;
    public Graph(int V) 
    {
        this.V = V;
        adj = new ArrayList<>(V);     
        for (int i = 0; i < V; i++)
            adj.add(new LinkedList<>());
    }
}
```

```java
private boolean isCyclic() {
    // Mark all the vertices as not visited and
    // not part of recursion stack
    boolean[] visited = new boolean[V];
    boolean[] recStack = new boolean[V];

    // Call the recursive helper function to
    // detect cycle in different DFS trees
    for (int i = 0; i < V; i++)
        if (isCyclicUtil(i, visited, recStack))
            return true;

    return false;
}

private boolean isCyclicUtil(int i, boolean[] visited, boolean[] recStack) {         
    // Mark the current node as visited and
    // part of recursion stack
    if (recStack[i])
        return true; //If we reach a vertex that is already in the recursion stack

    if (visited[i])
        return false;

    visited[i] = true;
    
    recStack[i] = true;
    List<Integer> children = adj.get(i);
    for (Integer c: children)
        if (isCyclicUtil(c, visited, recStack))
                    return true;
    recStack[i] = false;

    return false;
}
```



