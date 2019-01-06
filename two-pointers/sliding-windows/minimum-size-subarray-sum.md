# [Minimum Size Subarray Sum](https://www.lintcode.com/problem/minimum-size-subarray-sum)

Given an array of n positive integers and a positive integer s, find the minimal length of a subarray of which the sum ≥ s. If there isn't one, return -1 instead.

### Example

Given the array`[2,3,1,2,4,3]`and s =`7`, the subarray`[4,3]`has the minimal length under the problem constraint.

### Note

求最小窗口的长度，维护的是满足条件的和

### Code 

```java
public class Solution {
    /**
     * @param nums: an array of integers
     * @param s: An integer
     * @return: an integer representing the minimum size of subarray
     */
    public int minimumSize(int[] nums, int s) {
        // write your code here
        int len = nums.length;
        int res = Integer.MAX_VALUE;
        int j = 0, sum = 0;
        for (int i = 0; i < len; i++) {
            while (j < len && sum < s) {
                sum += nums[j];
                j++;
            }
            
            if (sum >= s) {
                res = Math.min(res, j - i);
            }
            
            sum -= nums[i];
        }
        
        return res == Integer.MAX_VALUE ? -1 : res;
    }
}
```



