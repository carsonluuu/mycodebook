# [LFU Cache](https://leetcode.com/problems/lfu-cache/description/)

Design and implement a data structure for [Least Frequently Used \(LFU\)](https://en.wikipedia.org/wiki/Least_frequently_used) cache. It should support the following operations: `get`and`put`.

`get(key)`- Get the value \(will always be positive\) of the key if the key exists in the cache, otherwise return -1.  
`put(key, value)`- Set or insert the value if the key is not already present. When the cache reaches its capacity, it should invalidate the least frequently used item before inserting a new item. For the purpose of this problem, when there is a tie \(i.e., two or more keys that have the same frequency\), the least **recently **used key would be evicted.

**Follow up:**  
Could you do both operations in**O\(1\)**time complexity?

### **Example**

```
LFUCache cache = new LFUCache( 2 /* capacity */ );

cache.put(1, 1);
cache.put(2, 2);
cache.get(1);       // returns 1
cache.put(3, 3);    // evicts key 2
cache.get(2);       // returns -1 (not found)
cache.get(3);       // returns 3.
cache.put(4, 4);    // evicts key 1.
cache.get(1);       // returns -1 (not found)
cache.get(3);       // returns 3
cache.get(4);       // returns 4
```

### Note



### Code

```java
/*
      Increasing frequencies
  ----------------------------->

+------+    +---+    +---+    +---+
| Head |----| 1 |----| 5 |----| 9 |  Frequencies
+------+    +-+-+    +-+-+    +-+-+
              |        |        |
            +-+-+    +-+-+    +-+-+     |
            |2,3|    |4,3|    |6,2|     |
            +-+-+    +-+-+    +-+-+     | Most recent 
                       |        |       |
                     +-+-+    +-+-+     |
 key,value pairs     |1,2|    |7,9|     |
                     +---+    +---+     v
*/

class LFUCache {
    class Entry {
        int key;
        int val;
        int count;
        Entry(int k, int v, int c) {
            key = k;
            val = v;
            count = c;
        }
    }
    
    // for key and value
    private HashMap<Integer, Entry> cache;
    // for freq and elems
    private HashMap<Integer, LinkedHashSet<Entry>> countMap;
    // capacity
    private int capacity;
    // min freq
    private int min = -1;
    
    public LFUCache(int capacity) {
        this.capacity = capacity;
        cache = new HashMap<>();
        countMap = new HashMap<>();
        countMap.put(1, new LinkedHashSet<>());
    }
    
    public int get(int key) {
        // key not found
        if (!cache.containsKey(key)) {
            return -1;
        }
        // remove in the original freq
        Entry e = cache.get(key);
        countMap.get(e.count).remove(e);
        // min is evicted up, then min needs add one
        if (e.count == min && countMap.get(e.count).isEmpty()) {
            countMap.remove(e.count);
            min++;
        }
        
        //update the freq after adding one
        e.count++;
        if (!countMap.containsKey(e.count)) {
            countMap.put(e.count, new LinkedHashSet<>());
        }
        countMap.get(e.count).add(e);
        
        return e.val;
    }
    
    public void put(int key, int value) {
        if (capacity <= 0) return;
        // 1. having the key then we update (need to get(key) to add freq)
        if (cache.containsKey(key)) {
            Entry e = cache.get(key);
            e.val = value;
            get(key);
            return;
        }
        // 2. evicting the least freq one
        if (cache.size() == capacity) {
            Iterator<Entry> it = countMap.get(min).iterator();
            Entry e = it.next();
            it.remove();
            cache.remove(e.key);
            // set empty then remove key
            if (!it.hasNext()) countMap.remove(min);
        }
        
        // 3. new one is created
        Entry newE = new Entry(key, value, 1);
        cache.put(key, newE);
        min = 1;
        // for the case we remove 1
        if (!countMap.containsKey(1)) {
            countMap.put(1, new LinkedHashSet<>());
        }
        countMap.get(1).add(newE);
    }
}

/**
 * Your LFUCache object will be instantiated and called as such:
 * LFUCache obj = new LFUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
```



