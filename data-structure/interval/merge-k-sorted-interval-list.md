# [Merge K Sorted Interval Lists](https://www.lintcode.com/problem/merge-k-sorted-interval-lists/description)

Merge\_K\_sorted interval lists into one sorted interval list. You need to merge overlapping intervals too.

### Example

Given

```
[
  [(1,3),(4,7),(6,8)],
  [(1,2),(9,10)]
]
```

Return

```
[(1,3),(4,8),(9,10)]
```

### Note

这里提供的是最后再进行merge的版本

更好的见[Merge k Sorted Intervals](/data-structure/merge/merge-k-sorted-intervals.md "Merge K Sorted Interval Lists")

### Code

```java
/**
 * Definition of Interval:
 * public classs Interval {
 *     int start, end;
 *     Interval(int start, int end) {
 *         this.start = start;
 *         this.end = end;
 *     }
 * }
 */

public class Solution {
    class Pair {
        public int row, col;
        public Pair(int row, int col) {
            this.row = row;
            this.col = col;
        }
    }
    /**
     * @param intervals: the given k sorted interval lists
     * @return:  the new sorted interval list
     */
    public List<Interval> mergeKSortedIntervalLists(List<List<Interval>> intervals) {
        // write your code here
        List<Interval> res = new ArrayList<>();
        int k = intervals.size();
        PriorityQueue<Pair> pq = new PriorityQueue<>(
            k, (a, b) -> 
            intervals.get(a.row).get(a.col).start - 
            intervals.get(b.row).get(b.col).start
        );

        for (int i = 0; i < k; i++) {
            if (intervals.get(i).size() > 0) {
                pq.add(new Pair(i, 0));
            }
        }

        while (!pq.isEmpty()) {
            Pair curr = pq.poll();
            res.add(intervals.get(curr.row).get(curr.col));
            curr.col++;
            if (curr.col < intervals.get(curr.row).size()) {
                pq.add(curr);
            }
        }

        return merge(res);

    }

    private List<Interval> merge(List<Interval> list) {
        if (list.size() <= 1) {
            return list;
        }

        List<Interval> res = new ArrayList<>();
        Interval last = list.get(0);
        for (int i = 1; i < list.size(); i++) {
            Interval curr = list.get(i);
            if (last.end < curr.start) {
                res.add(last);
                last = curr;
            } else {
                last.end = Math.max(last.end, curr.end);
            }
        }

        res.add(last);

        return res;
    }

}
```



