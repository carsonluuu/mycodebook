# Merge Sort

```java
public class Solution {
    /**
     * @param A: an integer array
     * @return: nothing
     */
    public void sortIntegers(int[] A) {
        // write your code here
        int[] temp = new int[A.length];
        mergeSort(A, 0, A.length - 1, temp);
    }
    
    private static void mergeSort(int[] A, int start, int end, int[] temp) {
        if (start >= end) {
            return;
        }
        
        mergeSort(A, start, (start + end) / 2, temp);
        mergeSort(A, (start + end) / 2 + 1, end, temp);
        merge(A, start, end, temp);
    }
    
    private static void merge(int[] A, int start, int end, int[] temp) {
        int mid = (start + end) / 2;
        int leftIndex = start;
        int rightIndex = mid + 1;
        int index = leftIndex;
        
        while (leftIndex <= mid && rightIndex <= end) {
            if (A[leftIndex] < A[rightIndex]) {
                temp[index++] = A[leftIndex++];
            } else {
                temp[index++] = A[rightIndex++];
            }
        }
        while (leftIndex <= mid) {
            temp[index++] = A[leftIndex++];
        }
        while (rightIndex <= end) {
            temp[index++] = A[rightIndex++];
        }
        
        for (int i = start; i <= end; i++) {
            A[i] = temp[i];
        }
    }
}
```



