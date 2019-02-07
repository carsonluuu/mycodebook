# [Interval List Intersections](https://leetcode.com/problems/interval-list-intersections/description/)

Given two lists of **closed **intervals, each list of intervals is pairwise disjoint and in sorted order.

Return the intersection of these two interval lists.

_\(Formally, a closed interval_`[a, b]`_\(with_`a <= b`_\) denotes the set of real numbers_`x`_with_`a <= x <= b`_.  The intersection of two closed intervals is a set of real numbers that is either empty, or can be represented as a closed interval.  For example, the intersection of \[1, 3\] and \[2, 4\] is \[2, 3\].\)_

### **Example**

![](https://assets.leetcode.com/uploads/2019/01/30/interval1.png)

### Note

双指针移动的标准是end谁小谁移动

### Code

```
Input: 
A = 
[[0,2],[5,10],[13,23],[24,25]]
, B = 
[[1,5],[8,12],[15,24],[25,26]]
Output: 
[[1,2],[5,5],[8,10],[15,23],[24,24],[25,25]]
Reminder: 
The inputs and the desired output are lists of Interval objects, and not arrays or lists.
```

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
class Solution {
    public Interval[] intervalIntersection(Interval[] A, Interval[] B) {
        List<Interval> res = new ArrayList<>();
        int i = 0, j = 0;
        while (i < A.length && j < B.length) {
            int start = Math.max(A[i].start, B[j].start);
            int end = Math.min(A[i].end, B[j].end);
            if (end >= start) {
                // intersect
                res.add(new Interval(start, end));
            }
            if (A[i].end < B[j].end) {
                i++;
            } else {
                j++;
            }
        }
        
        return res.toArray(new Interval[res.size()]);
    }
}
```



