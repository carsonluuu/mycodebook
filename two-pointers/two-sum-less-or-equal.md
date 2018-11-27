# Two Sum - Less than or equal to target

Given an array of integers, find how many pairs in the array such that their sum is`less than or equal to`a specific target number. Please return the number of pairs.

### Example

Given nums =`[2, 7, 11, 15]`, target =`24`.  
Return`5`.  
2 + 7 &lt; 24  
2 + 11 &lt; 24  
2 + 15 &lt; 24  
7 + 11 &lt; 24  
7 + 15 &lt; 25

### Note

小于的话：

```java
if (nums[left] + nums[right] <= target) {
    res += right - left;
    left++;
}
```

### Code

```java
public class Solution {
    /**
     * @param nums: an array of integer
     * @param target: an integer
     * @return: an integer
     */
    public int twoSum5(int[] nums, int target) {
        // write your code here
        // 2 7 11 15
        if (nums == null || nums.length < 2) {
            return 0;
        }
        Arrays.sort(nums);
        int res = 0;
        int left = 0, right = nums.length - 1;
        while (left < right) {
            if (nums[left] + nums[right] <= target) {
                res += right - left;
                left++;
            } else {
                right--;
            }
        }
        return res;
    }
}
```



