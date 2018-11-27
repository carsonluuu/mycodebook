# Shortest Path in Undirected Graph

Give an`undirected graph`, in which each edge's length is`1`, and give`two`nodes from the graph. We need to find the`length`of`the shortest path`between the given`two`nodes.

### Example

Given graph =`{1,2,4#2,1,4#3,5#4,1,2#5,3}`, and nodeA =`3`, nodeB =`5`.

```
1------2  3
 \     |  | 
  \    |  |
   \   |  |
    \  |  |
      4   5
```

return`1`

### Code

```java
public class Solution {
    /**
     * @param graph: a list of Undirected graph node
     * @param A: nodeA
     * @param B: nodeB
     * @return:  the length of the shortest path
     */
    public int shortestPath(List<UndirectedGraphNode> graph, UndirectedGraphNode A, UndirectedGraphNode B) {
        // Write your code here
        Queue<UndirectedGraphNode> queue = new LinkedList<>();
        Set<UndirectedGraphNode> set = new HashSet<>();
        queue.offer(A);
        set.add(A);

        int result = 0;

        while (!queue.isEmpty()) {
            int size = queue.size();
            result++;
            for (int i = 0; i < size; i++) {
                UndirectedGraphNode current = queue.poll();
                for (UndirectedGraphNode n : current.neighbors) {
                    if (set.contains(n)) {
                        continue;
                    }
                    if (n.label == B.label) {
                        return result;
                    }

                    queue.offer(n);
                    set.add(n);
                }
            }
        }

        return -1;
    }
}
```

双向宽度优先搜索 \(**Bidirectional BFS**\) 算法适用于如下的场景：

1. 无向图
2. 所有边的长度都为 1 或者长度都一样
3. 同时给出了起点和终点

以上 3 个条件都满足的时候，可以使用双向宽度优先搜索来求出起点和终点的最短距离。

### 算法描述

双向宽度优先搜索本质上还是BFS，只不过变成了起点向终点和终点向起点同时进行扩展，直至两个方向上出现同一个子节点，搜索结束。我们还是可以利用队列来实现：一个队列保存从起点开始搜索的状态，另一个保存从终点开始的状态，两边如果相交了，那么搜索结束。起点到终点的最短距离即为起点到相交节点的距离与终点到相交节点的距离之和。

**Q.双向BFS是否真的能提高效率？**  
假设单向BFS需要搜索 N 层才能到达终点，每层的判断量为 X，那么总的运算量为X ^ N. 如果换成是双向BFS，前后各自需要搜索 N / 2 层，总运算量为2 \* X ^ {N / 2}。如果 N 比较大且X 不为 1，则运算量相较于单向BFS可以大大减少，差不多可以减少到原来规模的根号的量级。

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



