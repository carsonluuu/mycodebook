# Moving Zeros

Given an array`nums`, write a function to move all`0`'s to the end of it while maintaining the relative order of the non-zero elements.

### Example

Given`nums = [0, 1, 0, 3, 12]`, after calling your function,`nums`should be`[1, 3, 12, 0, 0]`.

### Note

when not zero override the value of the left and right pointer will go through the array; give 0 for ones after left pointer

swap with left when not zero and right pointer will go through the array \(quicker\)

### Code

```java
public class Solution {
    /**
     * @param nums: an integer array
     * @return: nothing
     */
    public void moveZeroes(int[] nums) {
        // write your code here
        /*
        [1, 3, 0, 0, 12]
               l
                     r
        */
        if (nums == null || nums.length == 0) return;
        int l = 0, r = 0;
        while (r < nums.length) {
            if (nums[r] != 0) {
                nums[l++] = nums[r];
            }
            r++;
        }
        while (l < nums.length) {
            nums[l++] = 0;
        }
    }
}
```

```java
public class Solution {
    /**
     * @param nums an integer array
     * @return nothing, do this in-place
     */
    public void moveZeroes(int[] nums) {
        // Write your code here
        int left = 0, right = 0;
        while (right < nums.length) {
            if (nums[right] != 0) {
                int temp = nums[left];
                nums[left] = nums[right];
                nums[right] = temp;
                left++;
            }
            right++;
        }
    }
}
```



