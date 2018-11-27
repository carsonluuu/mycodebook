# Union-Find

### 简介

底层数据结构

* 父亲表示法，用一个数组/哈希表记录每个节点的父亲是谁。
* father\[“Nokia”\] = “Microsoft”
* father\[“Instagram”\] = “Facebook”

查询所在集合

* 用所在集合最顶层的老大哥节点来代表这个集合

合并两个集合

* 找到两个集合中最顶层的两个老大哥节点 A 和 B
* father\[A\] = B // or father\[B\] = A 如果无所谓谁合并谁的话

使用哈希表或者数组来存储每个节点的父亲节点， 如果节点不是连续整数的话，就最好用哈希表来存储，最开始所有的父亲节点都指向自己

**Find** **路径压缩** —— 在找到老大哥以后，还需要把一路上经过的点都指向老大哥

**Union **—— 找到两个元素所在集合的两个老大哥 A 和 B， 将其中一个老大哥的父指针指向另外一个老大哥

Time 都是 O\(log\* n\)，约等于 O\(1\)

### 功能

1. 合并两个集合

2. 查询某个元素所在集合

3. 判断两个元素是否在同一个集合

4. 获得某个集合的元素个数

5. 统计当前集合个数

跟连通性有关的问题，都可以使用 BFS 和 Union Find

什么时候无法使用 Union Find?

* 需要拆开两个集合的时候无法使用Union Find

### 示例一 - 判断两个点是否联通

```java
public class ConnectingGraph {
    /*
    * @param n: An integer
    */
    private int[] father;
    public ConnectingGraph(int n) {
        // do intialization if necessary
        father = new int[n + 1];
        for (int i = 1; i <= n; i++) {
            father[i] = i;
        }
    }

    private int find(int x) {
        if (father[x] == x) {
            return father[x];
        }
        father[x] = find(father[x]);

        return father[x];
    } 

    /*
     * @param a: An integer
     * @param b: An integer
     * @return: nothing
     */
    public void connect(int a, int b) {
        // write your code here
        int root_a = find(a);
        int root_b = find(b);
        if (root_a != root_b) {
            father[root_a] = root_b;
        }
    }

    /*
     * @param a: An integer
     * @param b: An integer
     * @return: A boolean
     */
    public boolean query(int a, int b) {
        // write your code here
        return find(a) == find(b);
    }
}
```

### 示例二 - 返回联通块大小

```java
public class ConnectingGraph2 {
    /*
    * @param n: An integer
    */
    int[] father;
    int[] size;
    public ConnectingGraph2(int n) {
        // do intialization if necessary
        father = new int[n + 1];
        size = new int[n + 1];
        for (int i = 1; i <= n; i++) {
            father[i] = i;
            size[i] = 1;
        }
    }

    /*
     * @param a: An integer
     * @param b: An integer
     * @return: nothing
     */

    private int find(int x) {
        if (father[x] == x) {
            return father[x];
        }

        father[x] = find(father[x]);
        return father[x];
    }

    public void connect(int a, int b) {
        // write your code here
        int root_a = find(a);
        int root_b = find(b);
        if (root_a != root_b) {
            father[root_a] = root_b;
            size[root_b] += size[root_a];
        }
    }

    /*
     * @param a: An integer
     * @return: An integer
     */
    public int query(int a) {
        // write your code here
        return size[find(a)];
    }
}
```

### 示例三 - 联通块总数

```java
public class ConnectingGraph3 {
    /**
     * @param a: An integer
     * @param b: An integer
     * @return: nothing
     */
    int count;
    int[] father;

    public ConnectingGraph3(int n) {
        father = new int[n + 1];
        count = n;
        for (int i = 1; i <= n; i++) {
            father[i] = i;
        }
    }

    public void connect(int a, int b) {
        // write your code here
        int root_a = find(a);
        int root_b = find(b);
        if (root_a != root_b) {
            count--;
            father[root_a] = root_b;
        }
    }

    /**
     * @return: An integer
     */
    public int query() {
        // write your code here
        return count;
    }


    private int find(int x) {
        if (father[x] == x) {
            return father[x];
        }

        return father[x] = find(father[x]);
    }
}
```

### 抽象并查集

还有一类数组题目利用扩展联通的思想，和Union-Find非常像的，下面罗列一下：

* TBD



