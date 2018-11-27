# Contiguous Array

Given a binary array, find the maximum length of a contiguous subarray with equal number of 0 and 1.

### Example

**Example 1:**

```
Input: [0,1]
Output: 2
Explanation: [0, 1] is the longest contiguous subarray with equal number of 0 and 1.
```

**Example 2:**

```
Input: [0,1,0]
Output: 2
Explanation: [0, 1] (or [1, 0]) is a longest contiguous subarray with equal number of 0 and 1.
```

### Note

Presum方法

sum 为 0：就是从0开始的答案（这里没有设置0的时候的sum）

记录sum出行的第一次值，sum值再次出现，计算最大长度

### Code

```java
class Solution {
    public int findMaxLength(int[] nums) {
        Map<Integer, Integer> map = new HashMap<>();
        int sum = 0, res = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == 0) {
                nums[i] = -1;
            }
        }
        
        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];
            if (sum == 0) {
                res = i + 1;
            } else if (map.containsKey(sum - 0)) {
                res = Math.max(res, i - map.get(sum - 0));
            }
            if (!map.containsKey(sum)) {
                map.put(sum, i);
            }
        }
        return res;
    }
}
```

  




