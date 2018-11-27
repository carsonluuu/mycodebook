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



