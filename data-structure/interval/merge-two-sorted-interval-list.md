# [Merge Two Sorted Interval Lists](https://www.lintcode.com/problem/merge-two-sorted-interval-lists/description)

Merge two sorted \(ascending\) lists of interval and return it as a new sorted list. The new sorted list should be made by splicing together the intervals of the two lists and sorted in ascending order.

### Example

Given list1 =`[(1,2),(3,4)]`and list2 =`[(2,3),(5,6)]`, return`[(1,4),(5,6)]`.

### Note

* buffer一个last
* 每个list维护一个头指针，取start较小的作为curr，与last进行merge，结果更新为新的last
* 对于merge子函数，当前的curr与last没有交集时，把last加入结果，返回last作为新的curr；否则对last进行合并与更新
* 记得加回去最后一个非null的last
* ### Code

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
     * @param list1: one of the given list
     * @param list2: another list
     * @return: the new sorted list of interval
     */
    public List<Interval> mergeTwoInterval(List<Interval> list1, 
                                           List<Interval> list2) {
        // write your code here
        List<Interval> res = new ArrayList<>();
        if (list1 == null || list2 == null) {
            return res;
        }
        Interval last = null, curr = null;
        int i = 0, j = 0;
        while (i < list1.size() && j < list2.size()) {
            if (list1.get(i).start < list2.get(j).start) {
                curr = list1.get(i);
                i++;
            } else {
                curr = list2.get(j);
                j++;
            }
            
            last = merge(res, last, curr);
        }
        
        while (i < list1.size()) {
            last = merge(res, last, list1.get(i++));
        }
        
        while (j < list2.size()) {
            last = merge(res, last, list2.get(j++));
        }
        
        if (last != null) {
            res.add(last);
        }
        
        return res;
    }
    
    private Interval merge(List<Interval> res, 
                           Interval last, Interval curr) {
        if (last == null) {
            return curr;
        }
        
        if (curr.start > last.end) {
            res.add(last);
            return curr;
        }
        
        last.end = Math.max(last.end, curr.end);
        
        return last;
    }
}
```



