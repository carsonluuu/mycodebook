### HASH

| Get | Find | Add/Remove | Space |
| :--- | :--- | :--- | :--- |
| O\(N/Bucket\_size\) | O\(N/Bucket\_size\) | O\(N/Bucket\_size\) | O\(N\) |

可以看出HashMap整体上性能都非常不错，但是不稳定，为O\(N/Buckets\)，N就是以数组中没有发生碰撞的元素，Buckets是因碰撞产生的链表。\(发生碰撞实际上是非常稀少的，所以N/Bucket\_size约等于1\)

### 哈希函数（Hash Function）

Keys -&gt; Hashing Function\(sha1/sha2/md5\) -&gt; Buckets

In data structure Hash, hash function is used to convert a string\(or any other type\) into an integer smaller than hash size and bigger or equal to zero. The objective of designing a hash function is to "hash" the key as unreasonable as possible. A good hash function can avoid collision as less as possible. A widely used hash function algorithm is using a magic number 33, consider any string as a 33 based big integer like follow:

hashcode\("abcd"\) = \(ascii\(a\) \* 33^3+ ascii\(b\) \* 33^2+ ascii\(c\) \* 33^1 + ascii\(d\) \* 33^0\) % HASH\_SIZE

```
                          = (97* 33^3+ 98 * 33^2 + 99 * 33 +100) % HASH_SIZE

                          = 3595978 % HASH_SIZE
```

here HASH\_SIZE is the capacity of the hash table \(you can assume a hash table is like an array with index 0 ~ HASH\_SIZE-1\).

### 冲突（Collision\)

是说两个不同的 key 经过哈希函数的计算后，得到了两个相同的值。解决冲突的方法，主要有两种：

1. 开散列法（Open Hashing）。是指哈希表所基于的数组中，每个位置是一个 Linked List 的头结点。这样冲突的 &lt;key, value&gt;  二元组，就都放在同一个链表中。
2. 闭散列法（Closed Hashing）。是指在发生冲突的时候，后来的元素，往下一个位置去找空位。

### 重哈希（Rehashing）

The size of the hash table is not determinate at the very beginning. If the total size of keys is too large \(e.g. size &gt;= capacity / 10\), we should double the size of the hash table and rehash every keys.

### HashMap与HashTable的主要区别 {#65-hashmap与hashtable的主要区别}

在很多的Java基础书上都已经说过了，他们的主要区别其实就是Table全局加了线程同步保护

* HashTable线程更加安全，代价就是因为它粗暴的添加了同步锁，所以会有性能损失。
* 其实有更好的concurrentHashMap可以替代HashTable，一个是方法级，一个是Class级。



