# House Robber II

After robbing those houses on that street, the thief has found himself a new place for his thievery so that he will not get too much attention. This time, all houses at this place are**arranged in a circle**. That means the first house is the neighbor of the last one. Meanwhile, the security system for these houses remain the same as for those in the previous street.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight**without alerting the police**.

### Example

nums =`[3,6,4]`, return`6`

### Note

环形，其实就是第一个抢还是不抢的问题。

也可以理解为在任意一个地点分裂，方便而言这里选择第一个。

### Code

```java
public class Solution {
    /**
     * @param nums: An array of non-negative integers.
     * @return: The maximum amount of money you can rob tonight
     */
    public int houseRobber2(int[] nums) {
        // write your code here
        if (nums == null || nums.length == 0) {
            return 0;
        }
        if (nums.length == 1) {
            return nums[0];
        }
        return Math.max(rob(nums, 0, nums.length - 1), 
                        rob(nums, 1, nums.length));
        
    }
    
    public int rob(int[] nums, int start, int end) {
    // write your code here
        int n = end;

        int twoPrev = 0;
        int onePrev = nums[start];
        for (int i = start + 2; i <= n; i++) {
            int curr = Math.max(onePrev, twoPrev + nums[i - 1]);
            twoPrev = onePrev;
            onePrev = curr;
        }
        return onePrev;
    }
}
```



