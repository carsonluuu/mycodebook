# Search Range

Given a sorted array of _n _integers, find the starting and ending position of a given target value.

If the target is not found in the array, return`[-1, -1]`.

### Example

Given`[5, 7, 7, 8, 8, 10]`and target value`8`,  
return`[3, 4]`.

### Code

```java
public class Solution {
    /**
     * @param A: an integer sorted array
     * @param target: an integer to be inserted
     * @return: a list of length 2, [index1, index2]
     */
    public int[] searchRange(int[] nums, int target) {
        // write your code here
        if (nums == null || nums.length == 0) {
            return new int[]{-1, -1};
        }
        
        int first = searchFirst(nums, target);
        int last = searchLast(nums, target);
        
        return new int[]{first, last};
    }
    
    private int searchFirst(int[] nums, int target) {
        int start = 0, end = nums.length - 1;
        while (start + 1 < end) {
            int mid = (end - start) / 2 + start;
            if (nums[mid] == target) {
                end = mid;
            } else if (nums[mid] < target) {
                start = mid;
            } else {
                end = mid;
            }
        }
        
        if (nums[start] == target) {
            return start;
        }
        if (nums[end] == target) {
            return end;
        }
        
        return -1;
    }
    
    private int searchLast(int[] nums, int target) {
        int start = 0, end = nums.length - 1;
        while (start + 1 < end) {
            int mid = (end - start) / 2 + start;
            if (nums[mid] == target) {
                start = mid;
            } else if (nums[mid] < target) {
                start = mid;
            } else {
                end = mid;
            }
        }
        
        if (nums[end] == target) {
            return end;
        }
        if (nums[start] == target) {
            return start;
        }
        
        return -1;
    }
}
```



