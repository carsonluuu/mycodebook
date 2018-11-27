# BFS模版

### 无需分层

```
// T 指代任何你希望存储的类型
Queue<T> queue = new LinkedList<>();
Set<T> set = new HashSet<>();

set.add(start);
queue.offer(start);
while (!queue.isEmpty()) {
    T head = queue.poll();
    for (T neighbor : head.neighbors) {
        if (!set.contains(neighbor)) {
            set.add(neighbor);
            queue.offer(neighbor);
        }
    }
}
```

上述代码中：

* neighbor 表示从某个点 head 出发，可以走到的下一层的节点。
* set 存储已经访问过的节点（已经丢到 queue 里去过的节点）
* queue 存储等待被拓展到下一层的节点
* set 与 queue 是一对好基友，无时无刻都一起出现，往 queue 里新增一个节点，就要同时丢到 set 里。

### 需要分层遍历的宽度搜先搜索

```
// T 指代任何你希望存储的类型
Queue<T> queue = new LinkedList<>();
Set<T> set = new HashSet<>();

set.add(start);
queue.offer(start);
while (!queue.isEmpty()) {
    int size = queue.size();
    for (int i = 0; i < size; i++) {
        T head = queue.poll();
        for (T neighbor : head.neighbors) {
            if (!set.contains(neighbor)) {
                set.add(neighbor);
                queue.offer(neighbor);
            }
        }
    }
}
```

上述代码中：

* size = queue.size\(\) 是一个必须的步骤。如果在 for 循环中使用`for (int i = 0; i <queue.size(); i++)`
  会出错，因为 queue.size\(\) 是一个动态变化的值。所以必须先把当前层一共有多少个节点存在局部变量 size 中，才不会把下一层的节点也在当前层进行扩展。



