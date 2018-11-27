# Bipartite

A [Bipartite Graph](http://en.wikipedia.org/wiki/Bipartite_graph) is a graph whose vertices can be divided into two independent sets, U and V such that every edge \(u, v\) either connects a vertex from U to V or a vertex from V to U.In other words, for every edge \(u, v\), either u belongs to U and v to V, or u belongs to V and v to U. We can also say that there is no edge that connects vertices of same set.

[![](https://cdncontribute.geeksforgeeks.org/wp-content/uploads/bipartitegraph-1.jpg "Bipartite1")](https://cdncontribute.geeksforgeeks.org/wp-content/uploads/bipartitegraph-1.jpg)

A bipartite graph is possible if the graph coloring is possible using two colors such that vertices in a set are colored with the same color. Note that it is possible to color a cycle graph with even cycle using two colors. For example, see the following graph.

[![](https://cdncontribute.geeksforgeeks.org/wp-content/uploads/bipartitegraphfive.sixJPG.jpg "Bipartite2")](https://cdncontribute.geeksforgeeks.org/wp-content/uploads/bipartitegraphfive.sixJPG.jpg)

It is not possible to color a cycle graph with odd cycle using two colors.  
[![](https://cdncontribute.geeksforgeeks.org/wp-content/uploads/bipartitegraphfive.jpg "Bipartite3")](https://cdncontribute.geeksforgeeks.org/wp-content/uploads/bipartitegraphfive.jpg)

_Algorithm to check if a graph is Bipartite:_  
One approach is to check whether the graph is 2-colorable or not using [backtracking algorithm m coloring problem](https://www.geeksforgeeks.org/backttracking-set-5-m-coloring-problem/).  
Following is a simple algorithm to find out whether a given graph is Birpartite or not using Breadth First Search \(BFS\).  
1. Assign RED color to the source vertex \(putting into set U\).  
2. Color all the neighbors with BLUE color \(putting into set V\).  
3. Color all neighbor’s neighbor with RED color \(putting into set U\).  
4. This way, assign color to all vertices such that it satisfies all the constraints of m way coloring problem where m = 2.  
5. While assigning colors, **if we find a neighbor which is colored with same color as current vertex**, then the graph cannot be colored with 2 vertices \(or graph is not Bipartite\)

