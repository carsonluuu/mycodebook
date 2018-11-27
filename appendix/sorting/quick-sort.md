# Quick Sort

1. left &lt;= right  错开
2. A\[left\] &lt; pivot, A\[right\] &gt; pivot 找到大于等于/小于等于 -- 均分
3. pivot -&gt; start and end
4. start-right, left-end

```java
public class Solution {
    /**
     * @param A: an integer array
     * @return: nothing
     */
    public void sortIntegers2(int[] A) {
        // write your code here
        quickSort(A, 0, A.length - 1);
    }

    private void quickSort(int[] A, int start, int end) {
        if (start >= end) {
            return;
        }

        int pivot = A[(start + end) / 2];
        int left = start, right = end;
        while (left <= right) {
            while (left <= right && A[left] < pivot) {
                left++;
            }
            while (left <= right && A[right] > pivot) {
                right--;
            }
            if (left <= right) {
                int temp = A[left];
                A[left++] = A[right];
                A[right--] = temp;
            }
        }
        quickSort(A, start, right);
        quickSort(A, left, end);
    }
}
```



