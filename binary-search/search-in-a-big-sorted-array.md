# Search in a Big Sorted Array

Given a big sorted array with positive integers sorted by ascending order. The array is so big so that you can not get the length of the whole array directly, and you can only access the kth number by`ArrayReader.get(k)`\(or ArrayReader-&gt;get\(k\) for C++\). Find the first index of a target number. Your algorithm should be in O\(log k\), where k is the first index of the target number.

Return -1, if the number doesn't exist in the array.

### Example

Given`[1, 3, 6, 9, 21, ...]`, and target =`3`, return`1`.

Given`[1, 3, 6, 9, 21, ...]`, and target =`4`, return`-1`

### Note

倍分法，先以跨度加倍的方式\(即index位置为1, 2, 4, 8…..2^x, 2^\(x+1\)\), 找到第一个比target大的数，再二分查找target

### Code

```java
public class Solution {
    /*
     * @param reader: An instance of ArrayReader.
     * @param target: An integer
     * @return: An integer which is the first index of target.
     */
    public int searchBigSortedArray(ArrayReader reader, int target) {
        // write your code here
        int i = 1;
        while (reader.get(i - 1) < target) {
            i *= 2;
        }
        int start = i / 2 - 1, end = i - 1;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (reader.get(mid) < target) {
                start = mid;
            } else {
                end = mid;
            }
        }
        if (reader.get(start) == target) {
            return start;
        }

        if (reader.get(end) == target) {
            return end;
        }
        return -1;
    }
}
```



