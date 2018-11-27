# [Insert Interval](https://leetcode.com/problems/insert-interval/description/)

Given a set of _non-overlapping _intervals, insert a new interval into the intervals \(merge if necessary\).

You may assume that the intervals were initially sorted according to their start times.

**Example 1:**

```
Input: intervals = [[1,3],[6,9]], newInterval = [2,5]

Output: [[1,5],[6,9]]
```

**Example 2:**

```
Input: intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]

Output: [[1,2],[3,10],[12,16]]

Explanation: Because the new interval [4,8] overlaps with [3,5],[6,7],[8,10].
```

### Note

找到插入的起点：直到条件不成立`intervals.get(i).end < newInterval.start`

插入：只要`intervals.get(i).start <= newInterval.end`就更新start和end

* newInterval.start = Math.min\(intervals.get\(i\).start, newInterval.start\);
* newInterval.end   = Math.max\(intervals.get\(i\).end,   newInterval.end\);

加入剩下的区间

### Code

```java
class Solution {
    public List<Interval> insert(List<Interval> intervals, Interval newInterval) {
        if (newInterval == null) {
            return intervals;
        }
        List<Interval> res = new ArrayList<>();
        
        int i = 0;
        int len = intervals.size();
        
        while (i < len && intervals.get(i).end < newInterval.start) {
            res.add(intervals.get(i++));
        }
        while (i < len && intervals.get(i).start <= newInterval.end) {
            newInterval.start = Math.min(intervals.get(i).start, newInterval.start);
            newInterval.end   = Math.max(intervals.get(i).end,   newInterval.end);
            i++;
        }
        
        res.add(newInterval);
        
        while (i < len) {
            res.add(intervals.get(i++));
        }
        return res;
    }
}
```



