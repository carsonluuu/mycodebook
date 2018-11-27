# Continuous Subarray Sum

Given a list of **non-negative **numbers and a target **integer **k, write a function to check if the array has a continuous subarray of size at least 2 that sums up to the multiple of **k **, that is, sums up to n\*k where n is also an **integer**

### Example

```
Input:
 [23, 2, 4, 6, 7],  k=6

Output:
 True

Explanation:
 Because [2, 4] is a continuous subarray of size 2 and sums up to 6.
```

```
Input:
 [23, 2, 6, 4, 7],  k=6

Output:
 True

Explanation:
 Because [23, 2, 6, 4, 7] is an continuous subarray of size 5 and sums up to 42.
```

1. The length of the array won't exceed 10,000.
2. You may assume the sum of all the numbers is in the range of a signed 32-bit integer.

### Note

`If presum1%k = c and presum2%k = c then |presum1 - presum2|%k=0`

注意一是0的位置在这里得初始化为-1，二是注意0的情况\[0, 0\], k = 0，输出是true，如果k是0的话就不取模了，三是注意间隔大于1，意味着presume的差不是单个元素。

### Code

```java
class Solution {
    public boolean checkSubarraySum(int[] nums, int k) {
        int sum = 0;
        Map<Integer, Integer> map = new HashMap<>();
        map.put(0, -1);
        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];
            int remainder = sum;
            if (k != 0) {
                remainder = sum % k;
            } 
            if (map.containsKey(remainder)) {
                if (i - map.get(remainder) > 1) {
                    return true;
                }
            } else {
                map.put(remainder, i);
            }
        }

        return false;
    }
}
```



