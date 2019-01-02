# Interval

```java
/**
 * Definition for an interval.
 * public class Interval {
 *     int start;
 *     int end;
 *     Interval() { start = 0; end = 0; }
 *     Interval(int s, int e) { start = s; end = e; }
 * }
 */
```

### Overlapping

按照区间起始值排序，重叠的条件是：如果前一个区间的end大于后一个区间的start，那么一定是重复区间。

`intervals[i].start < intervals[last].end`

在这个条件下，维护end更大的区间，缓存为last

`intervals[i].end < intervals[last].end`

### Sweep Line

一种区间的遍历



