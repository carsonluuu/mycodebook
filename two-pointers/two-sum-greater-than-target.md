# Two Sum - Greater than target

Given an array of integers, find how many pairs in the array such that their sum is bigger than a specific target number. Please return the number of pairs.

Do it in O\(1\) extra space and O\(nlogn\) time.

### Example

Given numbers =`[2, 7, 11, 15]`, target =`24`. Return`1`. \(11 + 15 is the only pair\)

### Note

大于的话

```java
if (nums[left] + nums[right] > target) { 
    count += right - left;
    right--;
}
```

### Code

```java
public class Solution {
    /**
     * @param nums: an array of integer
     * @param target: An integer
     * @return: an integer
     */
    public int twoSum2(int[] nums, int target) {
        // write your code here
        if (nums == null || nums.length < 2) {
            return 0;
        }
        
        Arrays.sort(nums);
        int left = 0, right = nums.length - 1;
        int count = 0;
        while (left < right) {
            if (nums[left] + nums[right] <= target) {
                left++;
            } else {
                count += right - left;
                right--;
            }
        }
        return count;
    }
}
```



