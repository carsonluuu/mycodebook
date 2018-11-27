# [3Sum Smaller](https://leetcode.com/problems/3sum-smaller/description/)

Given an array ofnintegersnumsand atarget, find the number of index triplets`i, j, k`with`0 <= i < j < k < n`that satisfy the condition `nums[i] + nums[j] + nums[k] < target`.

### **Example**

```
Input: nums = [-2,0,1,3], and target = 2

Output: 2 

Explanation: Because there are two triplets which sums are less than 2:
             [-2,0,1]
             [-2,0,3]
```

### Note

固定一个数，做2sum smaller

### Code

```java
class Solution {
    public int threeSumSmaller(int[] nums, int target) {
        int res = 0;
        if (nums == null || nums.length < 3) {
            return res;
        }

        Arrays.sort(nums);
        int len = nums.length;
        for (int i = 0; i < len - 2; i++) {
            int low = i + 1, high = len - 1, sum = target - nums[i];
            while (low < high) {
                if (nums[low] + nums[high] < sum) {
                    res += high - low;
                    low++;
                } else {
                    high--;
                }
            }
        }

        return res;
    }
}
```



