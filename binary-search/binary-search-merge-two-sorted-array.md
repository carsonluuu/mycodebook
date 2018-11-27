# Merge Two Sorted Arrays

Merge two given sorted integer array\_A\_and\_B\_into a new sorted integer array.

### Example

A=`[1,2,3,4]`

B=`[2,4,5,6]`

return`[1,2,2,3,4,4,5,6]`

### Code

Optimize algorithm if one array is very large and the other is very small \(B is smaller one assuming\)

```java
public class Solution {
    /*
     * @param A: sorted integer array A
     * @param B: sorted integer array B
     * @return: A new sorted integer array
     */
    public int[] mergeSortedArray(int[] A, int[] B) {
        if (A == null || A.length == 0) return B;
        if (B == null || B.length == 0) return A;
        int[] res = new int[A.length + B.length];
        int idx = 0;
        int startA = 0;
        for (int i = 0; i < B.length; i++) {
            int position = findHigherClosest(A, B[i]);
            while (startA < position) {
                res[idx++] = A[startA++];
            }
            res[idx++] = B[i];
        }
        while (startA < A.length){
            res[idx++] = A[startA++];
        }
        return res;
    }
    
    //Find the first element larger than target
    private int findHigherClosest(int[] nums, int target) {
        int start = 0, end = nums.length - 1;
        while (start + 1 < end) {
            int mid = (end - start) / 2 + start;
            if (nums[mid] <= target) {
                start = mid;
            } else {
                end = mid;
            }
        }
    
        if (nums[start] > target) {
            return start;
        }
        if (nums[end] > target) {
            return end;
        }
    
        return nums.length;
    }
}
```



