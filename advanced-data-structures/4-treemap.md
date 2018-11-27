# [TreeSet](https://docs.oracle.com/javase/7/docs/api/java/util/TreeSet.html)/[TreeMap](https://docs.oracle.com/javase/7/docs/api/java/util/TreeMap.html)

TreeSet / TreeMap 是底层运用了[红黑树](https://zh.wikipedia.org/wiki/%E7%BA%A2%E9%BB%91%E6%A0%91)的数据结构

#### 对比 HashSet / HashMap

* HashSet / HashMap 存取的时间复杂度为**O\(1\)**,而 TreeSet / TreeMap 存取的时间复杂度为**O\(logn\)**所以在存取上并不占优。
* HashSet / HashMap 内元素是无序的，而TreeSet / TreeMap 内部是有序的\(可以是按自然顺序排列也可以自定义排序\)。
* TreeSet / TreeMap 还提供了类似[lowerBound](http://www.cplusplus.com/reference/algorithm/lower_bound/)和[upperBound](http://www.cplusplus.com/reference/algorithm/upper_bound/)这两个其他数据结构没有的方法
  * 对于 TreeSet, 实现上述两个方法的方法为：
    * **lowerBound**
      * **public E lower\(E e\) **--&gt; 返回set中**严格小于**给出元素的**最大元素**，如果没有满足条件的元素则返回**null**。
      * **public E floor\(E e\) **--&gt; 返回set中**不大于**给出元素的**最大元素**，如果没有满足条件的元素则返回**null**。
    * **upperBound**
      * **public E higher\(E e\) **--&gt; 返回set中**严格大于**给出元素的**最小元素**，如果没有满足条件的元素则返回**null**。
      * **public E ceiling\(E e\) **--&gt; 返回set中**不小于**给出元素的**最小元素**，如果没有满足条件的元素则返回**null**。
  * 对于 TreeMap, 实现上述两个方法的方法为：
    * **lowerBound**
      * **public Map.Entry&lt;K,V&gt; lowerEntry\(K key\) **--&gt; 返回map中**严格小于**给出的key值的**最大key**对应的**key-value对**，如果没有满足条件的key则返回**null**。
      * **public K lowerKey\(K key\) **--&gt; 返回map中**严格小于**给出的key值的**最大key**，如果没有满足条件的key则返回**null**。
      * **public Map.Entry&lt;K,V&gt; floorEntry\(K key\) **--&gt; 返回map中**不大于**给出的key值的**最大key**对应的**key-value对**，如果没有满足条件的key则返回**null**。
      * **public K floorKey\(K key\) **--&gt; 返回map中**不大于**给出的key值的**最大key**，如果没有满足条件的key则返回**null**。
    * **upperBound**
      * **public Map.Entry&lt;K,V&gt; higherEntry\(K key\) **--&gt; 返回map中**严格大于**给出的key值的**最小key**对应的**key-value对**，如果没有满足条件的key则返回**null**。
      * **public K higherKey\(K key\) **--&gt; 返回map中**严格大于**给出的key值的**最小key**，如果没有满足条件的key则返回**null**。
      * **public Map.Entry&lt;K,V&gt; ceilingEntry\(K key\)**--&gt; 返回map中**不小于**给出的key值的**最小key**对应的**key-value对**，如果没有满足条件的key则返回**null**。
      * **public K ceilingKey\(K key\) **--&gt; 返回map中**不小于**给出的key值的**最小key**，如果没有满足条件的key则返回**null**。
  * lowerBound 与 upperBound 均为二分查找\(因此要求有序\)，时间复杂度为**O\(logn\)**.

#### 对比 PriorityQueue\(Heap\)

**PriorityQueue**是基于Heap实现的，它可以保证队头元素是优先级最高的元素，但其余元素是不保证有序的。

* 方法时间复杂度对比：
  * 添加元素 add\(\) / offer\(\)
    * TreeSet: O\(logn\)
    * PriorityQueue: O\(logn\)
  * 删除元素 poll\(\) / remove\(\)
    * TreeSet: O\(logn\)
    * PriorityQueue: O\(n\)
  * 查找 contains\(\)
    * TreeSet: O\(logn\)
    * PriorityQueue: O\(n\)
  * 取最小值 first\(\) / peek\(\)
    * TreeSet: O\(logn\)
    * PriorityQueue: O\(1\)

#### 常见用法

比如滑动窗口需要保证有序，那么这时可以用到TreeSet,因为TreeSet是有序的，并且不需要每次移动窗口都重新排序，只需要插入和删除\(O\(logn\)\)就可以了

### Doc Intro

A Red-Black tree based[`NavigableMap`](https://docs.oracle.com/javase/8/docs/api/java/util/NavigableMap.html)implementation. The map is sorted according to the [natural ordering](https://docs.oracle.com/javase/8/docs/api/java/lang/Comparable.html) of its keys, or by a [`Comparator`](https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html) provided at map creation time, depending on which constructor is used.

This implementation provides guaranteed log\(n\) time cost for the `containsKey`,`get`,`put`and`remove`operations.

**Note that this implementation is not synchronized**

```
public class TreeMap<K,V>   Set<Map.Entry<K,V>>
extends AbstractMap<K,V>
implements NavigableMap<K,V>, Cloneable, Serializable
```

### Methods

* ceilingKey/floorKey -&gt; include equal
* lower/highrt -&gt; strictly

| Modifier and Type | Method and Description |
| :--- | :--- |
| [`Map.Entry`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.Entry.html)`<`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`,`[`V`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`>` | [`ceilingEntry`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#ceilingEntry-K-)`(`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`key)`Returns a key-value mapping associated with the least key greater than or equal to the given key, or`null`if there is no such key. |
| [`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html) | [`ceilingKey`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#ceilingKey-K-)`(`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`key)`Returns the least key greater than or equal to the given key, or`null`if there is no such key. |
| `void` | [`clear`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#clear--)`()`Removes all of the mappings from this map. |
| [`Object`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html) | [`clone`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#clone--)`()`Returns a shallow copy of this`TreeMap`instance. |
| [`Comparator`](https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html)`<? super`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`>` | [`comparator`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#comparator--)`()`Returns the comparator used to order the keys in this map, or`null`if this map uses the[natural ordering](https://docs.oracle.com/javase/8/docs/api/java/lang/Comparable.html)of its keys. |
| `boolean` | [`containsKey`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#containsKey-java.lang.Object-)`(`[`Object`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html)`key)`Returns`true`if this map contains a mapping for the specified key. |
| `boolean` | [`containsValue`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#containsValue-java.lang.Object-)`(`[`Object`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html)`value)`Returns`true`if this map maps one or more keys to the specified value. |
| [`NavigableSet`](https://docs.oracle.com/javase/8/docs/api/java/util/NavigableSet.html)`<`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`>` | [`descendingKeySet`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#descendingKeySet--)`()`Returns a reverse order[`NavigableSet`](https://docs.oracle.com/javase/8/docs/api/java/util/NavigableSet.html)view of the keys contained in this map. |
| [`NavigableMap`](https://docs.oracle.com/javase/8/docs/api/java/util/NavigableMap.html)`<`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`,`[`V`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`>` | [`descendingMap`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#descendingMap--)`()`Returns a reverse order view of the mappings contained in this map. |
| [`Set`](https://docs.oracle.com/javase/8/docs/api/java/util/Set.html)`<`[`Map.Entry`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.Entry.html)`<`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`,`[`V`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`>>` | [`entrySet`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#entrySet--)`()`Returns a[`Set`](https://docs.oracle.com/javase/8/docs/api/java/util/Set.html)view of the mappings contained in this map. |
| [`Map.Entry`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.Entry.html)`<`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`,`[`V`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`>` | [`firstEntry`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#firstEntry--)`()`Returns a key-value mapping associated with the least key in this map, or`null`if the map is empty. |
| [`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html) | [`firstKey`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#firstKey--)`()`Returns the first \(lowest\) key currently in this map. |
| [`Map.Entry`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.Entry.html)`<`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`,`[`V`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`>` | [`floorEntry`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#floorEntry-K-)`(`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`key)`Returns a key-value mapping associated with the greatest key less than or equal to the given key, or`null`if there is no such key. |
| [`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html) | [`floorKey`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#floorKey-K-)`(`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`key)`Returns the greatest key less than or equal to the given key, or`null`if there is no such key. |
| `void` | [`forEach`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#forEach-java.util.function.BiConsumer-)`(`[`BiConsumer`](https://docs.oracle.com/javase/8/docs/api/java/util/function/BiConsumer.html)`<? super`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`,? super`[`V`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`> action)`Performs the given action for each entry in this map until all entries have been processed or the action throws an exception. |
| [`V`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html) | [`get`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#get-java.lang.Object-)`(`[`Object`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html)`key)`Returns the value to which the specified key is mapped, or`null`if this map contains no mapping for the key. |
| [`SortedMap`](https://docs.oracle.com/javase/8/docs/api/java/util/SortedMap.html)`<`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`,`[`V`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`>` | [`headMap`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#headMap-K-)`(`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`toKey)`Returns a view of the portion of this map whose keys are strictly less than`toKey`. |
| [`NavigableMap`](https://docs.oracle.com/javase/8/docs/api/java/util/NavigableMap.html)`<`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`,`[`V`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`>` | [`headMap`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#headMap-K-boolean-)`(`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`toKey, boolean inclusive)`Returns a view of the portion of this map whose keys are less than \(or equal to, if`inclusive`is true\)`toKey`. |
| [`Map.Entry`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.Entry.html)`<`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`,`[`V`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`>` | [`higherEntry`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#higherEntry-K-)`(`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`key)`Returns a key-value mapping associated with the least key strictly greater than the given key, or`null`if there is no such key. |
| [`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html) | [`higherKey`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#higherKey-K-)`(`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`key)`Returns the least key strictly greater than the given key, or`null`if there is no such key. |
| [`Set`](https://docs.oracle.com/javase/8/docs/api/java/util/Set.html)`<`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`>` | [`keySet`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#keySet--)`()`Returns a[`Set`](https://docs.oracle.com/javase/8/docs/api/java/util/Set.html)view of the keys contained in this map. |
| [`Map.Entry`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.Entry.html)`<`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`,`[`V`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`>` | [`lastEntry`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#lastEntry--)`()`Returns a key-value mapping associated with the greatest key in this map, or`null`if the map is empty. |
| [`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html) | [`lastKey`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#lastKey--)`()`Returns the last \(highest\) key currently in this map. |
| [`Map.Entry`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.Entry.html)`<`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`,`[`V`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`>` | [`lowerEntry`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#lowerEntry-K-)`(`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`key)`Returns a key-value mapping associated with the greatest key strictly less than the given key, or`null`if there is no such key. |
| [`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html) | [`lowerKey`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#lowerKey-K-)`(`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`key)`Returns the greatest key strictly less than the given key, or`null`if there is no such key. |
| [`NavigableSet`](https://docs.oracle.com/javase/8/docs/api/java/util/NavigableSet.html)`<`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`>` | [`navigableKeySet`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#navigableKeySet--)`()`Returns a[`NavigableSet`](https://docs.oracle.com/javase/8/docs/api/java/util/NavigableSet.html)view of the keys contained in this map. |
| [`Map.Entry`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.Entry.html)`<`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`,`[`V`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`>` | [`pollFirstEntry`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#pollFirstEntry--)`()`Removes and returns a key-value mapping associated with the least key in this map, or`null`if the map is empty. |
| [`Map.Entry`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.Entry.html)`<`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`,`[`V`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`>` | [`pollLastEntry`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#pollLastEntry--)`()`Removes and returns a key-value mapping associated with the greatest key in this map, or`null`if the map is empty. |
| [`V`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html) | [`put`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#put-K-V-)`(`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`key,`[`V`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`value)`Associates the specified value with the specified key in this map. |
| `void` | [`putAll`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#putAll-java.util.Map-)`(`[`Map`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html)`<? extends`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`,? extends`[`V`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`> map)`Copies all of the mappings from the specified map to this map. |
| [`V`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html) | [`remove`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#remove-java.lang.Object-)`(`[`Object`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html)`key)`Removes the mapping for this key from this TreeMap if present. |
| [`V`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html) | [`replace`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#replace-K-V-)`(`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`key,`[`V`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`value)`Replaces the entry for the specified key only if it is currently mapped to some value. |
| `boolean` | [`replace`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#replace-K-V-V-)`(`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`key,`[`V`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`oldValue,`[`V`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`newValue)`Replaces the entry for the specified key only if currently mapped to the specified value. |
| `void` | [`replaceAll`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#replaceAll-java.util.function.BiFunction-)`(`[`BiFunction`](https://docs.oracle.com/javase/8/docs/api/java/util/function/BiFunction.html)`<? super`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`,? super`[`V`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`,? extends`[`V`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`> function)`Replaces each entry's value with the result of invoking the given function on that entry until all entries have been processed or the function throws an exception. |
| `int` | [`size`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#size--)`()`Returns the number of key-value mappings in this map. |
| [`NavigableMap`](https://docs.oracle.com/javase/8/docs/api/java/util/NavigableMap.html)`<`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`,`[`V`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`>` | [`subMap`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#subMap-K-boolean-K-boolean-)`(`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`fromKey, boolean fromInclusive,`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`toKey, boolean toInclusive)`Returns a view of the portion of this map whose keys range from`fromKey`to`toKey`. |
| [`SortedMap`](https://docs.oracle.com/javase/8/docs/api/java/util/SortedMap.html)`<`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`,`[`V`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`>` | [`subMap`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#subMap-K-K-)`(`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`fromKey,`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`toKey)`Returns a view of the portion of this map whose keys range from`fromKey`, inclusive, to`toKey`, exclusive. |
| [`SortedMap`](https://docs.oracle.com/javase/8/docs/api/java/util/SortedMap.html)`<`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`,`[`V`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`>` | [`tailMap`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#tailMap-K-)`(`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`fromKey)`Returns a view of the portion of this map whose keys are greater than or equal to`fromKey`. |
| [`NavigableMap`](https://docs.oracle.com/javase/8/docs/api/java/util/NavigableMap.html)`<`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`,`[`V`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`>` | [`tailMap`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#tailMap-K-boolean-)`(`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`fromKey, boolean inclusive)`Returns a view of the portion of this map whose keys are greater than \(or equal to, if`inclusive`is true\)`fromKey`. |
| [`Collection`](https://docs.oracle.com/javase/8/docs/api/java/util/Collection.html)`<`[`V`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`>` | [`values`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#values--)`()`Returns a[`Collection`](https://docs.oracle.com/javase/8/docs/api/java/util/Collection.html)view of the values contained in this map. |



