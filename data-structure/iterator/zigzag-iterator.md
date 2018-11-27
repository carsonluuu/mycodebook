# Zigzag Iterator

Given k 1d vectors, implement an iterator to return their elements alternately.

The "Zigzag" order is not clearly defined and is ambiguous for`k > 2`cases. If "Zigzag" does not look right to you, replace "Zigzag" with "Cyclic". For example:

```
Input:

[1,2,3]
[4,5,6,7]
[8,9]


Output: 
[1,4,8,2,5,9,3,6,7].
```

Uses a linkedlist to store the iterators in different vectors. Every time we call next\(\), we pop an element from the list, and re-add it to the end to cycle through the lists.

```java
public class ZigzagIterator {
    
    LinkedList<Iterator> list;
    
    public ZigzagIterator(List<Integer> v1, List<Integer> v2) {
        list = new LinkedList<Iterator>();
        if (!v1.isEmpty()) {
            list.add(v1.iterator());
        }
        if (!v2.isEmpty()) {
            list.add(v2.iterator());
        }
    }
    
    public int next() {
        Iterator it = list.remove();
        int res = (Integer)it.next();
        if (it.hasNext()) {
            list.add(it);
        }
        return res;
    }
    
    public boolean hasNext() {
        return !list.isEmpty();
    }
}
```



