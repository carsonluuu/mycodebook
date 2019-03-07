# [Longest Continuous Increasing Subsequence](https://leetcode.com/problems/longest-continuous-increasing-subsequence/description/)

Given an unsorted array of integers, find the length of longest`continuous`increasing subsequence \(subarray\).

# **Example**

**Example 1:**  


```
Input:
 [1,3,5,4,7]

Output:
 3

Explanation:
 The longest continuous increasing subsequence is [1,3,5], its length is 3. 
Even though [1,3,5,7] is also an increasing subsequence, it's not a continuous one where 5 and 7 are separated by 4. 

```



**Example 2:**  


```
Input:
 [2,2,2,2,2]

Output:
 1

Explanation:
 The longest continuous increasing subsequence is [2], its length is 1. 
```

### Note

1. DP
2. 双指针
3. 直接遍历，不符合条件就置0

### Code

```java
class Solution {
    public int findLengthOfLCIS(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;   
        }
        int n = nums.length, res = 1;
        int[] dp = new int[n];
        dp[0] = 1;
        for (int i = 1; i < n; i++) {
            if (nums[i] > nums[i - 1]) {
                dp[i] = dp[i - 1] + 1;
            } else {
                dp[i] = 1;
            }
            res = Math.max(res, dp[i]);
        }
        
        return res;
        
    }
}

class Solution {
    public int findLengthOfLCIS(int[] nums) {
        int ans = 0, anchor = 0;
        for (int i = 0; i < nums.length; ++i) {
            if (i > 0 && nums[i-1] >= nums[i]) anchor = i;
            ans = Math.max(ans, i - anchor + 1);
        }
        return ans;
    }
}

class Solution {
    public int findLengthOfLCIS(int[] nums) {
        int res = 0, cnt = 0;
        for (int i = 0; i < nums.length; i++){
            if (i == 0 || nums[i-1] < nums[i]) res = Math.max(res, ++cnt);
            else cnt = 1;
        }
        return res;
    }
}
```



