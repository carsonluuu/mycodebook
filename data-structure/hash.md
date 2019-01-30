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

### 问题

**1. 什么时候会使用HashMap？他有什么特点？**  
是基于Map接口的实现，存储键值对时，它可以接收null的键值，是非同步的，HashMap存储着Entry\(hash, key, value, next\)对象。

**2. 你知道HashMap的工作原理吗？**  
通过hash的方法，通过put和get存储和获取对象。存储对象时，我们将K/V传给put方法时，它调用hashCode计算hash从而得到bucket位置，进一步存储，HashMap会根据当前bucket的占用情况自动调整容量\(超过Load Facotr则resize为原来的2倍\)。获取对象时，我们将K传给get，它调用hashCode计算hash从而得到bucket位置，并进一步调用equals\(\)方法确定键值对。如果发生碰撞的时候，Hashmap通过链表将产生碰撞冲突的元素组织起来，在Java 8中，如果一个bucket中碰撞冲突的元素超过某个限制\(默认是8\)，则使用**红黑树来替换链表**，从而提高速度。

**3. 你知道get和put的原理吗？equals\(\)和hashCode\(\)的都有什么作用？**  
通过对key的hashCode\(\)进行hashing，并计算下标\( n-1 & hash\)，从而获得buckets的位置。如果产生碰撞，则利用key.equals\(\)方法去链表或树中去查找对应的节点

**4. 你知道hash的实现吗？为什么要这样实现？**  
在Java 1.8的实现中，是通过hashCode\(\)的高16位异或低16位实现的：`(h = k.hashCode()) ^ (h >>> 16)`，主要是从速度、功效、质量来考虑的，这么做可以在bucket的n比较小的时候，也能保证考虑到高低bit都参与到hash的计算中，同时不会有太大的开销。

**5. 如果HashMap的大小超过了负载因子\(load factor\)定义的容量，怎么办？**  
如果超过了负载因子\(默认0.75\)，则会重新resize一个原来长度两倍的HashMap，并且重新调用hash方法。

[关于Java集合的小抄](http://calvin1978.blogcn.com/articles/collection.html)中是这样描述的：

> 以Entry\[\]数组实现的哈希桶数组，用Key的哈希值取模桶数组的大小可得到数组下标。
>
> 插入元素时，如果两条Key落在同一个桶\(比如哈希值1和17取模16后都属于第一个哈希桶\)，Entry用一个next属性实现多个Entry以单向链表存放，后入桶的Entry将next指向桶当前的Entry。
>
> 查找哈希值为17的key时，先定位到第一个哈希桶，然后以链表遍历桶里所有元素，逐个比较其key值。
>
> 当Entry数量达到桶数量的75%时\(很多文章说使用的桶数量达到了75%，但看代码不是\)，会成倍扩容桶数组，并重新分配所有原来的Entry，所以这里也最好有个预估值。
>
> 取模用位运算\(hash & \(arrayLength-1\)\)会比较快，所以数组的大小永远是2的N次方， 你随便给一个初始值比如17会转为32。默认第一次放入元素时的初始值是16。
>
> iterator\(\)时顺着哈希桶数组来遍历，看起来是个乱序。
>
> 在JDK8里，新增默认为8的閥值，当一个桶里的Entry超过閥值，就不以单向链表而以红黑树来存放以加快Key的查找速度。



