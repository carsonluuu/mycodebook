### Meeting Rooms II

Given an array of meeting time intervals consisting of start and end times`[[s1,e1],[s2,e2],...] (si < ei)`, find the minimum number of conference rooms required.

### Example

Given intervals =`[(0,30),(5,10),(15,20)]`, return`2`.

### Note

找天上同时有多少架飞机，扫描线做，start：1/end：0来排序

主要根据题目不同情况看看边界怎么算，即相等怎么排序

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
    /**
     * @param intervals: an array of meeting time intervals
     * @return: the minimum number of conference rooms required
     */
    private static class Node {
        int val, flag;
        public Node(int val, int flag) {
            this.val = val;
            this.flag = flag;
        }
    }  
    public int minMeetingRooms(List<Interval> intervals) {
        // Write your code here
        int res = 0;
        if (intervals == null || intervals.size() == 0) {
            return res;
        }
        
        List<Node> sweep = new ArrayList<>();
        for (Interval elem : intervals) {
            sweep.add(new Node(elem.start, 1));
            sweep.add(new Node(elem.end, 0));
        }
        
        Collections.sort(sweep, (a, b) -> a.val == b.val ? a.flag - b.flag : a.val - b.val);
        int count = 0;
        for (Node elem : sweep) {
            if (elem.flag == 1) {
                count++;
            }
            else {
                count--;
            }
            res = Math.max(res, count);
        }
        
        return res;
    }
}
```



