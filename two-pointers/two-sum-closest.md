# Two Sum - Closest to Target

Given an array `nums`of _n _integers, find two integers in_nums_such that the sum is closest to a given number,_target_.

Return the difference between the sum of the two integers and the target.

### Example

Given array`nums`=`[-1, 2, 1, -4]`, and _target _=`4`.

The minimum difference is`1`. \(4 - \(2 + 1\) = 1\).

### Note

左边是越走越大的，右边是越走越小的。

* 相加小的话，想往右走，left加
* 相加大的话，想往左走，right减
* 维护一个最小的diff

### Code

```java
public class Solution {
    /**
     * @param nums: an integer array
     * @param target: An integer
     * @return: the difference between the sum and the target
     */
    public int twoSumClosest(int[] nums, int target) {
        // write your code here
        if (nums == null || nums.length < 2) {
            return -1;
        }
        Arrays.sort(nums);
        int left = 0, right = nums.length - 1;
        int diff = Integer.MAX_VALUE;
        // -4 -1 1 2  | 4
        while (left < right) {
            if (nums[left] + nums[right] < target) {
                diff = Math.min(diff, target - nums[left] - nums[right]);
                left++;
            } else {
                diff = Math.min(diff, nums[left] + nums[right] - target);
                right--;
            }
        }
        return diff;
    }
}
```



