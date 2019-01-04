# Non-overlapping Intervals

Given a collection of intervals, find the minimum number of intervals you need to remove to make the rest of the intervals non-overlapping.

1. You may assume the interval's end point is always bigger than its start point.
2. Intervals like \[1,2\] and \[2,3\] have borders "touching" but they don't overlap each other.

### Example

```
Input:
[ [1,2], [2,3], [3,4], [1,3] ]

Output:
1

Explanation:
[1,3] can be removed and the rest of intervals are non-overlapping.
```

```
Input:
[ [1,2], [1,2], [1,2] ]

Output:
2

Explanation:
You need to remove two [1,2] to make the rest of intervals non-overlapping.
```

```
Input:
[ [1,2], [2,3] ]

Output:
0

Explanation:
You don't need to remove any of the intervals since they're already non-overlapping.
```

### Note

这道题给了我们一堆区间，让我们求需要至少移除多少个区间才能使剩下的区间没有重叠，那么我们首先要给区间排序，根据每个区间的start来做升序排序，然后我们开始要查找重叠区间，判断方法是看如果前一个区间的end大于后一个区间的start，那么一定是重复区间，此时我们结果res自增1，我们需要删除一个，那么此时我们究竟该删哪一个呢，为了保证我们总体去掉的区间数最小，我们去掉那个end值较大的区间，而在代码中，我们并没有真正的删掉某一个区间，而是用一个变量last指向上一个需要比较的区间，我们将last指向end值较小的那个区间；如果两个区间没有重叠，那么此时last指向当前区间，继续进行下一次遍历

### Code

```
class Solution {
    public int eraseOverlapIntervals(Interval[] nums) {
        Arrays.sort(nums, (a, b) -> a.start - b.start);
        int res = 0;
        int last = 0;
        for (int i = 1; i < nums.length; i++) { 
            if (nums[i].start < nums[last].end) { //overlapping condition
                res++;
                if (nums[i].end < nums[last].end) {
                    last = i; //keep the smaller end
                }
            } else {
                last = i; //cache non-overlapping last
            }
        }

        return res;
    }
}
```



