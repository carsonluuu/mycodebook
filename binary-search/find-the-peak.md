# Find Peak Element

There is an integer array which has the following features:

* The numbers in adjacent positions are different
* A\[0\] &lt; A\[1\]  && A\[A.length - 2\]  &gt; A\[A.length - 1\]

We define a position P is a peak if:

```
A[P] > A[P-1] && A[P] > A[P+1]
```

Find a peak element in this array. Return the index of the peak.

### Example

Given`[1, 2, 1, 3, 4, 5, 7, 6]`

Return index`1`\(which is number 2\) or`6`\(which is number 7\)

### Note

A\[0\] &lt; A\[1\]  && A\[A.length - 2\]  &gt; A\[A.length - 1\]  说明至少有一个峰

### ![](/assets/findPeakElem.png)

对于一个不是中间的数,有如下四种情况，第一种直接返回, 其他情况,保留先增后减的一半.

如果中间的数比后一位数大的话，peek点肯定在mid左边或是mid

如果中间的数比前一位数小的话，peek点肯定在mid右边或是mid

 最后一种情况代表其他case，无所谓在哪边了

`start = 1, end = len - 2`

### Code

```java
public class Solution {
    /*
     * @param A: An integers array.
     * @return: return any of peek positions.
     */
    public int findPeak(int[] A) {
        // write your code here
        int start = 1, end = A.length - 2;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (A[mid] > A[mid - 1] && A[mid] > A[mid + 1]) {
                return mid;
            } else if (A[mid] < A[mid - 1]) {
                end = mid;
            } else if (A[mid] < A[mid + 1]) {
                start = mid;
            } else {
                end = mid;
            }
        }
        return A[start] > A[end] ? start : end;
    }
}
```



