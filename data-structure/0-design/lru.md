# [LRU](https://www.lintcode.com/problem/lru-cache/description)

Design and implement a data structure for Least Recently Used \(LRU\) cache. It should support the following operations: `get` and `set`.

`get(key)` - Get the value \(will always be positive\) of the key if the key exists in the cache, otherwise return -1.  
`set(key, value)` - Set or insert the value if the key is not already present. When the cache reached its capacity, it should invalidate the least recently used item before inserting a new item.

### Example

```java
LRUCache cache = new LRUCache(2);

cache.put(1, 1);
cache.put(2, 2);
cache.get(1);       // returns 1
cache.put(3, 3);    // evicts key 2
cache.get(2);       // returns -1 (not found)
cache.put(4, 4);    // evicts key 1
cache.get(1);       // returns -1 (not found)
cache.get(3);       // returns 3
cache.get(4);       // returns 4

 33
 44
```

### Note

这里操作都需要是常数时间的，使用一个LinkedHashMap记录元素的键和值，同时使用一个HashMap，记录这个键和其之前的节点，方便进行移动操作。

成员变量有总大小，当前大小，sentinel，tail 和 map：

```
private int capacity, size;
private ListNode sentinel, tail;
private Map<Integer, ListNode> map;
```

帮助函数`moveToTail(int key)`会移动这个键值的节点去尾部。删除并添加至尾部

两点注意：

* 一是尾部和当前相等时，直接退出，对应只有一个元素的情况
* 二是这个元素已经是最后一个元素了，这个时候`prev.next`会是`null`
* 三是删除的那个地方节点也要更新，map在二情况不出现的情况下更新两次

get函数map里没有这个元素会直接返回-1，否则调用帮助函数并且返回tail的值

set函数分为三种情况：

* 一是已经存在，那么直接更新并退出
* 二是不存在，但当前还没有满，那么更新tail和size，加入map
* 三是不存在，但是满了，那么要remove least recent，把原来的first删除，然后更新为当前的first，然后调用帮助函数移动到tail，map一次删除一次添加

### Code

```java
public class LRUCache {

    class ListNode {
        public int key, val;
        public ListNode next;

        public ListNode (int key, int val) {
            this.key = key;
            this.val = val;
            next = null;
        }
    }

    private int capacity, size;
    private ListNode sentinel, tail;
    private Map<Integer, ListNode> map; //key -> prev

    /*
    * @param capacity: An integer
    */
    public LRUCache(int capacity) {
        // do intialization if necessary
        this.capacity = capacity;
        map = new HashMap<>();
        sentinel = new ListNode(0, 0);
        tail = sentinel;
    }

    private void moveToTail(int key) {
        ListNode prev = map.get(key);
        ListNode curr = prev.next;

        if (tail == curr) {
            return;
        }

        prev.next = prev.next.next; //delete
        tail.next = curr; // add to tail

        if (prev.next != null) { //is last?
            map.put(prev.next.key, prev);
        }
        map.put(curr.key, tail);

        tail = curr;
    }

    /*
     * @param key: An integer
     * @return: An integer
     */
    public int get(int key) {
        // write your code here
        if (!map.containsKey(key)) {
            return -1;
        }

        moveToTail(key);

        return tail.val;
    }

    public void set(int key, int value) {
        // write your code here
        if (get(key) != -1) { //already exist
            ListNode prev = map.get(key);
            prev.next.val = value;
            return;
        }

        if (size < capacity) { // less than size add directly
            size++;
            ListNode curr = new ListNode(key, value);
            tail.next = curr;
            map.put(key, tail);

            tail = curr;
            return;
        }

        // third case: not exist and up to the cap -> remove least and add
        ListNode first = sentinel.next;
        map.remove(first.key);

        first.key = key;
        first.val = value;
        map.put(key, sentinel);

        moveToTail(key);
    }
}
```



