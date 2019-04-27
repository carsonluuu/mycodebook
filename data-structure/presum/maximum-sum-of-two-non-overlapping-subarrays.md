# [Maximum Sum of Two Non-Overlapping Subarrays](https://leetcode.com/problems/maximum-sum-of-two-non-overlapping-subarrays/description/)

Given an array`A`of non-negative integers, return the maximum sum of elements in two non-overlapping \(contiguous\) subarrays, which have lengths `L`and`M`.  \(For clarification, the`L`-length subarray could occur before or after the`M`-length subarray.\)

Formally, return the largest`V`for which `V = (A[i] + A[i+1] + ... + A[i+L-1]) + (A[j] + A[j+1] + ... + A[j+M-1])`and either:

### Example

**Example 1:**

```
Input: 
A = [0,6,5,2,2,5,1,9,4], L = 1, M = 2
Output: 
20

Explanation:
 One choice of subarrays is [9] with length 1, and [6,5] with length 2.
```

**Example 2:**

```
Input: 
A = [3,8,1,3,2,1,8,9,0], L = 3, M = 2
Output: 
29

Explanation:
 One choice of subarrays is
 [3,8,1] with length 3, and [8,9] with length 2.
```

**Example 3:**

```
Input: 
A = [2,1,5,6,0,9,5,0,3,8], L = 4, M = 3
Output: 
31

Explanation:
 One choice of subarrays is
 [5,6,0,9] with length 4, and [3,8] with length 3.
```

### Note

维护定长的MAX的preSum，同时维护一个最大的和

L和M谁在前面并不影响

### Code

```java
class Solution {
    /* L=3 M=5
      0   1  2  3   4    5   6   7   8   9  
     [4, 5, 14, 16, 16, 20,  7, 13,  8, 15]
      4  9  23  39  55  75   82 95  103 118
                L
    */
    public int maxSumTwoNoOverlap(int[] A, int L, int M) {
        int len = A.length;
        int[] sum = new int[len];
        sum[0] = A[0];
        
        for (int i = 1; i < len; ++i) {
            sum[i] = sum[i - 1] + A[i];
        }
        
        int res = 0;
        int Lmax = sum[L - 1], Mmax = sum[M - 1];
        for (int i = 0; i < len; ++i) {
            if (i >= L && i + M - 1 < len) {
                res = Math.max(res, Lmax + sum[i + M - 1] - sum[i - 1]);
            }
            
            if (i >= M && i + L - 1 < len) {
                res = Math.max(res, Mmax + sum[i + L - 1] - sum[i - 1]);
            }
            
            if (i >= L) {
                Lmax = Math.max(Lmax, sum[i] - sum[i - L]);
            }
            
            if (i >= M) {
                Mmax = Math.max(Mmax, sum[i] - sum[i - M]);
            }
        }
        return res;
    }
}
```



