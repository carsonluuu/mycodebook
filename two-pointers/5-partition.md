# Partition - 划分

是相向双指针的重点题型之二

一是经典的快速排序/快速选择算法

二是扩展到三个指针，如color sort甚至彩虹排序

### 快速选择

第k小

```java
public class Solution {
    /**
     * @param k: An integer
     * @param nums: An integer array
     * @return: kth smallest element
     */
    public int kthSmallest(int k, int[] nums) {
        // write your code here
        return quickSelect(nums, 0, nums.length - 1, k - 1);
    }
    
    private static int quickSelect(int[] A, int start, int end, int k) {
        if (start == end) {
            return A[start];
        }
        int left = start, right = end;
        int pivot = A[(left + right) / 2];
        
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
        
        //start      right   left      end
        //                 |
        
        if (right >= k && start <= right) {
            return quickSelect(A, start, right, k);
        } else if (left <= k && left <= end) {
            return quickSelect(A, left, end, k);
        } else {
            return A[k];
        }
    }
}
```

第k大

```java
class Solution {
    /*
     * @param k : description of k
     * @param nums : array of nums
     * @return: description of return
     */
    public int kthLargestElement(int k, int[] nums) {
        // write your code here
        return quickSelect(nums, 0, nums.length - 1, k);
    }
    
    private static int quickSelect(int[] nums, int start, 
                                 int end, int k) {
        if (start >= end) {
            return nums[start];
        }
        int left = start, right = end;
        int pivot = nums[(left + right) / 2];
        while (left <= right) {
            while (left <= right && nums[left] > pivot) {
                left++;
            }
            while (left <= right && nums[right] < pivot) {
                right--;
            }
            if (left <= right) {
                int temp = nums[left];
                nums[left++] = nums[right];
                nums[right--] = temp;
            }
        }
        
        if (start + k - 1 <= right) {
            return quickSelect(nums, start, right, k);
        }
        if (start + k - 1 >= left) {
            return quickSelect(nums, left, end, k - (left - start));
        }
        return nums[right + 1];
    }
}
```



