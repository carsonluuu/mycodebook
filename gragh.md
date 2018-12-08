# Graph

### Define

有很多种方法可以存储一个图，最常用的莫过于：

1. 邻接矩阵
2. 邻接表

而邻接矩阵因为耗费空间过大，我们通常在工程中都是使用邻接表作为图的存储结构。

**邻接矩阵 Adjacent Matrix**

```
[
  [1,0,0,1],
  [0,1,1,0],
  [0,1,1,0],
  [1,0,0,1]
]
```

例如上图表示0号点和3号点有连边。1号点和2号店有连边。  
当然，每个点和自己也是默认有连边的。  
图中的`0`表示不连通，`1`表示连通。  
我们也可以用一个更具体的整数值来表示连边的长度。  
邻接矩阵我们可以直接用一个二维数组表示，如`int[][] matrix;`。这种数据结构因为耗费 O\(n^2\) 的空间，所以在稀疏图上浪费很大，因此并不常用。

**邻接表 \(Adjacent List\)**

```
[
  [1],
  [0,2,3],
  [1],
  [1]
]
```

这个图表示 0 和 1 之间有连边，1 和 2 之间有连边，1 和 3 之间有连边。即每个点上存储自己有哪些邻居（有哪些连通的点）。  
这种方式下，空间耗费和边数成正比，可以记做 O\(m\)，m代表边数。m最坏情况下虽然也是 O\(n^2\)，但是邻接表的存储方式大部分情况下会比邻接矩阵更省空间。

#### 自定义邻接表

可以用自定义的类来实现邻接表

```
class DirectedGraphNode {
     int label;
     ArrayList<DirectedGraphNode> neighbors;
     DirectedGraphNode(int x) { label = x; neighbors = new ArrayList<DirectedGraphNode>(); }
}

class UndirectedGraphNode {
     int label;
     List<UndirectedGraphNode> neighbors;
     UndirectedGraphNode(int x) { label = x; neighbors = new ArrayList<UndirectedGraphNode>(); }
};
```

其中 neighbors 表示和该点连通的点有哪些。

#### 使用 Map 和 Set（面试时）

也可以使用 HashMap 和 HashSet 搭配的方式来存储邻接表

```
Map<T, Set<T>> = new HashMap<Integer, HashSet<Integer>>();
```

其中 T 代表节点类型。通常可能是整数\(Integer\)。  
这种方式虽然没有上面的方式更加直观和容易理解，但是在面试中比较节约代码量。  
而自定义的方法，更加工程化，所以在面试中如果时间不紧张题目不难的情况下，推荐使用自定义邻接表的方式。

#### 简化版

有的时候节点会简化成0-1000的数字，这时图的表示就比较简化了

```
Input: [[1,3], [0,2], [1,3], [0,2]]
Explanation: 
The graph looks like this:
0----1
|    |
|    |
3----2
```

```
Input: [[1,2,3], [0,2], [0,1,3], [0,2]]
Explanation: 
The graph looks like this:
0----1
| \  |
|  \ |
3----2
```

这种就是邻接表的一个例子，注意节点从1开始还是从0开始，有些情况会告诉最大节点数，方便初始化邻接表

#### **OJ's undirected graph serialization:**

Nodes are labeled uniquely.

We use`#`as a separator for each node, and`,`as a separator for node label and each neighbor of the node.

As an example, consider the serialized graph`{0,1,2#1,2#2,2}`.

The graph has a total of three nodes, and therefore contains three parts as separated by`#`.

1. First node is labeled as`0`. Connect node`0`to both nodes`1`and`2`
2. Second node is labeled as`1`. Connect node`1`to node`2`.
3. Third node is labeled as`2`. Connect node`2`to node`2`\(itself\), thus forming a self-cycle.

Visually, the graph looks like the following:

```
       1
      / \
     /   \
    0 --- 2
         / \
         \_/
```

### Some statement for tree in graph theory

> \(1\) A tree is an undirected graph in which any two vertices are connected by exactly one path.
>
> \(2\) Any connected graph who has`n`nodes with`n-1`edges is a tree.
>
> \(3\) The degree of a vertex of a graph is the number of edges incident to the vertex.
>
> \(4\) A leaf is a vertex of degree 1. An internal vertex is a vertex of degree at least 2.
>
> \(5\) A path graph is a tree with two or more vertices that is not branched at all.
>
> \(6\) A tree is called a rooted tree if one vertex has been designated the root.
>
> \(7\) The height of a rooted tree is the number of edges on the longest downward path between root and a leaf.

### BFS/DFS

Graph 是非常重要而又涵盖很广的内容，以至于有单独的 “图论” 研究方向。LeetCode 上很多问题都可以抽象成 “图” ，比如搜索类问题，树类问题，迷宫问题，矩阵路径问题，等等。

重点在于 DFS 和 BFS 的比较；可以看到；

* BFS 的时间空间占用以 branching factor 为底， 到解的距离 d 为指数增长；空间占用上 Queue 是不会像 DFS 一样只存一条路径的，而是从起点出发越扩越大，因此会有空间不够的风险，空间占用为 O\(b^d\)。
* DFS 的时间占用以 branching factor 为底，树的深度 m 为指数增长；而空间占用上，却只是 O\(bm\)，可视化探索过程中只把每个 Node 的所有子节点存在 Stack 上， 探索完了再 pop 出来接着探，因此储存的节点数为 O\(bm\)。

可以看到无论是 BFS 还是 DFS，树的 branching factor 都是对空间与时间复杂度影响最大的参数；除此之外，BFS 中最重要的是到解的距离，而 DFS 看从当前节点的深度。普遍来讲，DFS 空间上会经济一些，当然也要分情况讨论。

![](https://mnmunknown.gitbooks.io/algorithm-notes/content/TreeSearch.PNG)

Topological sort，拓扑排序，是 graph 搜索中一种特殊的顺序，本质上还是完全可以靠 BFS / DFS 解决。

**有向图 DFS 图示：**

![](https://mnmunknown.gitbooks.io/algorithm-notes/content/DFS.JPG)

**有向图 BFS 图示：**

![](https://mnmunknown.gitbooks.io/algorithm-notes/content/BFS.JPG)

**可以看到两种搜索都用了三种颜色表示状态。**

---

* **有向图 Directed：**

  * **DFS**:

    * Detect Cycle \([Course Schedule](https://leetcode.com/problems/course-schedule/)\)

      > * 暴力解法：DFS + Backtracking，寻找“所有从当前节点的” path，如果试图访问 visited 则有环；缺点是，同一个点会被探索多次，而且要从所有点作为起点保证算法正确性，时间复杂度非常高
      >
      > * 最优解法是 CLRS 上用三种状态表示每个节点：
      >   * "0" 还未访问过;
      >   * "1" 代表正在访问；
      >   * "2" 代表已经访问过；
      > * DFS 开始时把当前节点设为 "1";
      > * 在从任意节点出发的时候，如果我们试图访问一个状态为 "1" 的节点，都说明图上有环。
      > * 当前节点的 DFS 结束时，设为 "2";
      > * 在找环上，DFS 比起 BFS 最大的优点是"对路径有记忆"，DFS 记得来时的路径和导致环的位置，BFS 却不行。

    * [Topological Sort](http://www.lintcode.com/en/problem/topological-sorting/)

      > * 类似剥洋葱，可以选择任意点开始向里 DFS ，记录path，后面做的其他 DFS path 都放在之前结果的前面。\(CLRS有\)
      > * 等价做法是，把每次 DFS 探索中的 path 按照由内向外的顺序添加\(单序列反序\), 后进行的 DFS 结果放在之前运行完的结果后面\(全序列反序\)，然后 reverse 就好了，可以改良 ArrayList 添加的时间复杂度。
      > * 更简单的做法是用 Java 内置的 LinkedList，支持双端操作。

    * Count \# of connected components

    * Determine if A is reachable from B

  * **BFS**：

    * Detect Cycle \([Course Schedule](https://leetcode.com/problems/course-schedule/)\)

      > * 首先，在 DAG 上找环，DFS 要比 BFS 强。
      > * #### 其次重点注意，有向图靠 3 个状态 BFS 是不能正确判断是否有环的，要靠 indegree，一个例子是 【0, 1】 和 【1,0】，环在发现之前已经被标注为 state 2 了。 {#其次重点注意，有向图靠-3-个状态-bfs-是不能正确判断是否有环的，要靠-indegree，一个例子是-【0-1】-和-【10】，环在发现之前已经被标注为-state-2-了。}
      > * 扫一遍所有 edge，记录每个节点的 indegree.
      > * 在有向无环图中，一定会存在至少一个 indegree 为 0 的起点，将所有这样的点加入queue。
      > * 依次处理queue里的节点，把每次poll出来的节点的 children indegree -1. 减完之后如果 child 的 indegree = 0 了，就也放入队列。
      > * 如果图真的没有环，可以顺利访问完所有节点，如果还有剩的，说明图中有环，因为环上节点的 indegree 没法归 0.

    * [Topological Sort](http://www.lintcode.com/en/problem/topological-sorting/)

      > * 步骤同上，扫的时候按顺序 append 就好了。
      > * 类似于“剥洋葱”，从最外面一层出发，逐步向里。

    * Count \# of connected components

    * Determine if A is reachable from B

      > * 这个任务最适合用 BFS 做，从 B 做起点一路扫看看能不能扫到 A 就行了。

---

* **Un-directed:**

  无向图算法的整体思路和有向图基本一致，但是需要重点注意 正确处理 “原路返回” 的情况，免得死循环或者误报。

  在无向图的2个状态基础上增加一个 “正在访问” 的新状态，加上注意 prev 就可以了。

  * **DFS**:

    * Detect Cycle \([Graph Valid Tree](https://leetcode.com/problems/graph-valid-tree/)\)

      > * 用 int\[\] 表示每个点的状态，其中
      >   * 0 代表“未访问”；
      >   * 1 代表“访问中”；
      >   * 2 代表“已访问”；
      > * DFS call 里要传入 "prev节点" 参数，避免出现原路返回，或者回到前一个节点误判为有环。\(和 directed graph DFS 唯一的不同之处\)
      >
      > * 其他情况下，如果我们试图访问一个状态为 “1” 的节点，都可以说明图中有环。

    * Topological Sort

      > * 都无向图了，topological 。。。。

    * Count \# of connected components \([Graph Valid Tree](https://leetcode.com/problems/graph-valid-tree/)\)

    * Determine if A is reachable from B

  * **BFS：**

    * Detect Cycle \([Graph Valid Tree](https://leetcode.com/problems/graph-valid-tree/)\)

      > * 扫描所有 edges 记录图到底长啥样；
      > * 用 "0,1,2" states;
      > * 随便扔一个点进 queue，标记 "1"，然后 BFS，所有 child = "0" 的都加入队列
      > * #### 所有 child 都检查完之后，立刻把当前 node = 2，不然下一层 BFS 会回头去看自己然后误报。 {#所有-child-都检查完之后，立刻把当前-node--2，不然下一层-bfs-会回头去看自己然后误报。}
      > * 如果遇到 child = "1" 的说明有环

    * Topological Sort

      > * 都无向图了，topological 。。。。

    * Count \# of connected components \([Graph Valid Tree](https://leetcode.com/problems/graph-valid-tree/)\)

      > * 和 Detect Cycle 一样，同时记录下到底做了几次 BFS 才扫遍全图，图上就有几个 connected components

    * Determine if A is reachable from B

      > * BFS 搜到底看看能不能到就可以了，这个和只靠 g\(x\) 的 uniform-cost search 一致。





