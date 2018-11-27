# [Merge Intervals](https://leetcode.com/problems/merge-intervals/description/)

Given a collection of intervals, merge all overlapping intervals.

**Example 1:**

```
Input: [[1,3],[2,6],[8,10],[15,18]]

Output: [[1,6],[8,10],[15,18]]

Explanation: Since intervals [1,3] and [2,6] overlaps, merge them into [1,6].
```

**Example 2:**

```
Input: [[1,4],[4,5]]

Output: [[1,5]]

Explanation: Intervals [1,4] and [4,5] are considerred overlapping.
```

### Note

* Sorting according to the start 
* Buffer the start and end
* Merge when curr.start &lt;= buffer end otherwise result add buffer and assign new buffer start and end
* Remember to add last buffer

### Code

```java
class Solution {
    public List<Interval> merge(List<Interval> intervals) {
        if (intervals == null || intervals.size() <= 1) return intervals;
        Collections.sort(intervals, (a, b) -> a.start - b.start);
        int start = intervals.get(0).start;
        int end   = intervals.get(0).end;
        List<Interval> res = new ArrayList<>();
        for (Interval i : intervals) {
            if (i.start <= end)
                end = Math.max(end, i.end);
            else {
                res.add(new Interval(start, end));
                start = i.start;
                end   = i.end;
            }
        }
        res.add(new Interval(start, end));
        return res;
    }
}
```



