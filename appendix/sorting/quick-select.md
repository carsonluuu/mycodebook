# Quick Select

注意下标在终止情况下的位置，因为是left小于等于right，所以right在left的左边，中间可能有一个元素，我们抛弃不是答案的那一部分。平均时间复杂度是O\(n\).

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



