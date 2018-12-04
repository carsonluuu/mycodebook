# [Increasing Triplet Subsequence](https://leetcode.com/problems/increasing-triplet-subsequence/)

Given an unsorted array return whether an increasing subsequence of length 3 exists or not in the array.

Formally the function should:

```
Return true if there exists i, j, k 
such that arr[i] < arr[j] < arr[k] given 0 ≤ i < j < k ≤ n-1 else return false.
```

**Note: **Your algorithm should run in O\(n\) time complexity and O\(1\) space complexity.

### Example

**Example 1:**

```
Input: [1,2,3,4,5]
Output: true
```

**Example 2:**

```
Input: [5,4,3,2,1]
Output: false
```

### Note

常数个数版本单调栈，主要体会一下思路

### Code

```java
class Solution {
    public boolean increasingTriplet(int[] nums) {
        int small = Integer.MAX_VALUE;
        int big = small;
        for (int num : nums) {
            if (num < small) {
                small = num;
            } else if (num < big) {
                big = num;
            } else {
                return true;
            }
        }
        
        return false;
    }
}
```



