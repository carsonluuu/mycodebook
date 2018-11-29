# BFS

### 图的遍历 Traversal in Graph

图的遍历，比如给出无向连通图\(Undirected Connected Graph\)中的一个点，找到这个图里的所有点。这就是一个常见的场景。  
LintCode 上的[Clone Graph](http://www.lintcode.com/problem/clone-graph)就是一个典型的练习题。

更细一点的划分的话，这一类的问题还可以分为：

* 层级遍历 Level Order Traversal
* 由点及面 Connected Component
* 拓扑排序 Topological Sorting

**层级遍历**，也就是说我不仅仅需要知道从一个点出发可以到达哪些点，还需要知道这些点，分别离出发点是第几层遇到的，比如[Binary Tree Level Order Traversal](http://www.lintcode.com/problem/binary-tree-level-order-traversal/)就是一个典型的练习题。

**由点及面**，前面已经提到。

**拓扑排序**，让我们在后一节中展开描述。

### 最短路径 Shortest Path in Simple Graph

最短路径算法有很多种，BFS 是其中一种，但是他有特殊的使用场景，即必须是在简单图中求最短路径。  
大部分简单图中使用 BFS 算法时，都是无向图。当然也有可能是有向图，但是在面试中极少会出现。

什么是简单图（Simple Graph）？

即，图中每条边长度都是1（或边长都相同）。

### 双向宽度优先搜索算法

双向宽度优先搜索 \(Bidirectional BFS\) 算法适用于如下的场景：

1. 无向图
2. 所有边的长度都为 1 或者长度都一样
3. 同时给出了起点和终点

以上 3 个条件都满足的时候，可以使用双向宽度优先搜索来求出起点和终点的最短距离。

##### 算法描述

双向宽度优先搜索本质上还是BFS，只不过变成了起点向终点和终点向起点同时进行扩展，直至两个方向上出现同一个子节点，搜索结束。我们还是可以利用队列来实现：一个队列保存从起点开始搜索的状态，另一个保存从终点开始的状态，两边如果相交了，那么搜索结束。起点到终点的最短距离即为起点到相交节点的距离与终点到相交节点的距离之和。

**Q.双向BFS是否真的能提高效率？**  
假设单向BFS需要搜索 N 层才能到达终点，每层的判断量为 X，那么总的运算量为X ^ N. 如果换成是双向BFS，前后各自需要搜索 N / 2 层，总运算量为2 \* X ^ {N / 2}。如果 N 比较大且X 不为 1，则运算量相较于单向BFS可以大大减少，差不多可以**减少到原来规模的根号的量级**。

##### 参考代码

```java
/**
 * Definition for graph node.
 * class UndirectedGraphNode {
 *     int label;
 *     ArrayList<UndirectedGraphNode> neighbors;
 *     UndirectedGraphNode(int x) { 
 *         label = x; neighbors = new ArrayList<UndirectedGraphNode>(); 
 *     }
 * };
 */
public int doubleBFS(UndirectedGraphNode start, UndirectedGraphNode end) {
    if (start.equals(end)) {
        return 1;
    }
    // 起点开始的BFS队列
    Queue<UndirectedGraphNode> startQueue = new LinkedList<>();
    // 终点开始的BFS队列
    Queue<UndirectedGraphNode> endQueue = new LinkedList<>();
    startQueue.add(start);
    endQueue.add(end);
    int step = 0;
    // 记录从起点开始访问到的节点
    Set<UndirectedGraphNode> startVisited = new HashSet<>();
    // 记录从终点开始访问到的节点
    Set<UndirectedGraphNode> endVisited = new HashSet<>();
    startVisited.add(start);
    endVisited.add(end);
    while (!startQueue.isEmpty() || !endQueue.isEmpty()) {
        int startSize = startQueue.size();
        int endSize = endQueue.size();
        // 按层遍历
        step ++;
        for (int i = 0; i < startSize; i ++) {
            UndirectedGraphNode cur = startQueue.poll();
            for (UndirectedGraphNode neighbor : cur.neighbors) {
                if (startVisited.contains(neighbor)) {//重复节点
                    continue;
                } else if (endVisited.contains(neighbor)) {//相交
                    return step;
                } else {
                    startVisited.add(neighbor);
                    startQueue.add(neighbor);
                }
            }
        }
        step ++;
        for (int i = 0; i < endSize; i ++) {
            UndirectedGraphNode cur = endQueue.poll();
            for (UndirectedGraphNode neighbor : cur.neighbors) {
                if (endVisited.contains(neighbor)) {
                    continue;
                } else if (startVisited.contains(neighbor)) {
                    return step;
                } else {
                    endVisited.add(neighbor);
                    endQueue.add(neighbor);
                }
            }
        }    
    }
    return -1; // 不连通
}
```

**学习建议**

Bidirectional BFS 掌握起来并不是很难，算法实现上稍微复杂了一点（代码量相对单向 BFS 翻倍），掌握这个算法一方面加深对普通 BFS 的熟练程度，另外一方面，基本上写一次就能记住，如果在面试中被问到了如何优化 BFS 的问题，Bidirectional BFS 几乎就是标准答案了。

**参考资料**

[https://www.geeksforgeeks.org/bidirectional-search](https://www.geeksforgeeks.org/bidirectional-search)

**应用例题**

[Shortest Path in Undirected Graph](http://www.lintcode.com/zh-cn/problem/shortest-path-in-undirected-graph/)  
[Knight Shortest Path](http://www.lintcode.com/zh-cn/problem/knight-shortest-path/)  
[Knight Shortest Path II](http://www.lintcode.com/en/problem/knight-shortest-path-ii/)

### 使用 Dummy Node 进行 BFS

##### 什么是 Dummy Node

Dummy Node，翻译为哨兵节点。Dummy Node 一般本身不存储任何实际有意义的值，通常用作"占位"，或者链表的“虚拟头”。  
如很多的链表问题中，我们会在原来的头head的前面新增一个节点，这个节点没有任何值，但是 next 指向 head。这样就会方便对 head 进行删除或者在前面插入等操作。

```
head->node->node->node ...
=>
dummy->head->node->node->node...
```

##### Dummy Node 在 BFS 中如何使用

在 BFS 中，我们主要用 dummy node 来做占位符。即，在队列中每一层节点的结尾，都放一个`null`（or None in Python，nil in Ruby），来表示这一层的遍历结束了。这里 dummy node 就是一个 null。

```
// T 可以是任何你想存储的节点的类型
Queue<T> queue = new LinkedList<>();
queue.offer(startNode);
queue.offer(null);
currentLevel = 0;
// 因为有 dummy node 的存在，不能再用 isEmpty 了来判断是否还有没有拓展的节点了
while (queue.size() > 1) {
    T head = queue.poll();
    if (head == null) {
        currentLevel++;
        queue.offer(null);
        continue;
    }
    for (all neighbors of head) {
        queue.offer(neighbor);
    }
}
```

### 使用两个队列的BFS实现

我们可以将当前层的所有节点存在第一个队列中，然后拓展（Extend）出的下一层节点存在另外一个队列中。来回迭代，逐层展开。

参考代码如下：

```java
// T 表示任意你想存储的类型
Queue<T> queue1 = new LinkedList<>();
Queue<T> queue2 = new LinkedList<>();
queue1.offer(startNode);
int currentLevel = 0;

while (!queue1.isEmpty()) {
   int size = queue1.size();
    for (int i = 0; i < size; i++) {
        T head = queue1.poll();
        for (all neighbors of head) {
            queue2.offer(neighbor);
        }
    }
    Queue<T> temp = queue1;
    queue1 = queue2;
    queue2 = temp;

    queue2.clear();
    currentLevel++;
}
```



