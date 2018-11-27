# Topological Sorting

#### 定义

在图论中，由一个有向无环图的顶点组成的序列，当且仅当满足下列条件时，称为该图的一个拓扑排序（英语：Topological sorting）。

* 每个顶点出现且只出现一次；
* 若A在序列中排在B的前面，则在图中不存在从B到A的路径。

也可以定义为：拓扑排序是对有向无环图的顶点的一种排序，它使得如果存在一条从顶点A到顶点B的路径，那么在排序中B出现在A的后面。

\(来自[Wiki](https://zh.wikipedia.org/wiki/拓撲排序)\)

![](/assets/topologicalsorting.png)

For each directed edge

* `A -> B`in graph, A must before B in the order list.
* The first node in the order can be any node in the graph with no nodes direct to it.

The topological order can be:

```
[0, 1, 2, 3, 4, 5]
[0, 2, 3, 1, 5, 4]
...
```

#### 实际运用

拓扑排序 Topological Sorting 是一个经典的图论问题。他实际的运用中，拓扑排序可以做如下的一些事情：

* 检测编译时的循环依赖
* 制定有依赖关系的任务的执行顺序

#### 拓扑排序不是一种排序算法

虽然名字里有 Sorting，但是相比起我们熟知的 Bubble Sort, Quick Sort 等算法，Topological Sorting 并不是一种严格意义上的 Sorting Algorithm。

确切的说，`一张图的拓扑序列可以有很多个，也可能没有`。拓扑排序只需要找到其中`一个`序列，无需找到`所有`序列。

#### 入度与出度

在介绍算法之前，我们先介绍图论中的一个基本概念，`入度`和`出度`，英文为 in-degree & out-degree。  
在有向图中，如果存在一条有向边 A--&gt;B，那么我们认为这条边为 A 增加了一个出度，为 B 增加了一个入度。

#### 算法流程

拓扑排序的算法是典型的宽度优先搜索算法，其大致流程如下：

1. 统计所有点的入度，并初始化拓扑序列为空。
2. 将所有入度为 0 的点，也就是那些没有任何
   `依赖`
   的点，放到宽度优先搜索的队列中
3. 将队列中的点一个一个的释放出来，放到拓扑序列中，每次释放出某个点 A 的时候，就访问 A 的相邻点（所有A指向的点），并把这些点的入度减去 1。
4. 如果发现某个点的入度被减去 1 之后变成了 0，则放入队列中。
5. 直到队列为空时，算法结束，

#### 深度优先搜索的拓扑排序

深度优先搜索也可以做拓扑排序，不过因为不容易理解，也并不推荐作为拓扑排序的主流算法。

#### 宽度优先搜索的拓扑排序

```java
class DirectedGraphNode {
     int label;
     ArrayList<DirectedGraphNode> neighbors;
     DirectedGraphNode(int x) { label = x; neighbors = new ArrayList<DirectedGraphNode>(); }
};
```

```java
public class Solution {
    /**
     * @param graph: A list of Directed graph node
     * @return: Any topological order for the given graph.
     */    
    public ArrayList<DirectedGraphNode> topSort(ArrayList<DirectedGraphNode> graph) {
        // map 用来存储所有节点的入度，这里主要统计各个点的入度
        HashMap<DirectedGraphNode, Integer> map = new HashMap();
        for (DirectedGraphNode node : graph) {
            for (DirectedGraphNode neighbor : node.neighbors) {
                if (map.containsKey(neighbor)) {
                    map.put(neighbor, map.get(neighbor) + 1);
                } else {
                    map.put(neighbor, 1); 
                }
            }
        }

        // 初始化拓扑序列为空
        ArrayList<DirectedGraphNode> result = new ArrayList<DirectedGraphNode>();

        // 把所有入度为0的点，放到BFS专用的队列中
        Queue<DirectedGraphNode> q = new LinkedList<DirectedGraphNode>();
        for (DirectedGraphNode node : graph) {
            if (!map.containsKey(node)) {
                q.offer(node);
                result.add(node);
            }
        }

        // 每次从队列中拿出一个点放到拓扑序列里，并将该点指向的所有点的入度减1
        while (!q.isEmpty()) {
            DirectedGraphNode node = q.poll();
            for (DirectedGraphNode n : node.neighbors) {
                map.put(n, map.get(n) - 1);
                // 减去1之后入度变为0的点，也放入队列
                if (map.get(n) == 0) {
                    result.add(n);
                    q.offer(n);
                }
            }
        }

        return result;
    }
}
```



