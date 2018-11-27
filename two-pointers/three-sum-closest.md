# 3Sum Closest

Given an array S of_n_integers, find three integers in S such that the sum is closest to a given number, target. Return the sum of the three integers.

Challenge：O\(n^2\) time, O\(1\) extra space

### Example

For example, given array_S_=`[-1 2 1 -4]`, and target =`1`. The sum that is closest to the target is`2`._\(-1 + 2 + 1 = 2\)_.

### Note

for循环其中一个, 另外两个做2 sum closest

注意

```java
int res = nums[0] + nums[1] + nums[2];
if (Math.abs(target - sum) < Math.abs(target - res)) { res = sum; }
```

### Code

```java
public class Solution {
    /**
     * @param numbers: Give an array numbers of n integer
     * @param target: An integer
     * @return: return the sum of the three integers, the sum closest target.
     */
    public int threeSumClosest(int[] nums, int target) {
        // write your code here
        if (nums == null || nums.length < 3) {
            return -1;
        }
        
        Arrays.sort(nums);
        int res = nums[0] + nums[1] + nums[2];
        // -4 -1 1 2 |
        for (int i = 0; i < nums.length; i++) {
            int left = i + 1, right = nums.length - 1;
            while (left < right) {
                int sum = nums[i] + nums[left] + nums[right];
                if (Math.abs(target - sum) < Math.abs(target - res)) {
                    res = sum;
                } else if (sum < target) {
                    left++;
                } else {
                    right--;
                }
            }
        }
        
        return res;
    }
}
```



