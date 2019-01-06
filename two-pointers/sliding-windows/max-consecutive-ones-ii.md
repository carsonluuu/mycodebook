# [Max Consecutive Ones II](https://leetcode.com/problems/max-consecutive-ones-ii/description/)

Given a binary array, find the maximum number of consecutive 1s in this array if you can flip at most one 0.

**Note:**

* The input array will only contain`0`and`1`.
* The length of input array is a positive integer and will not exceed 10,000

### **Example**

```
Input:
 [1,0,1,1,0]

Output:
 4

Explanation:
 Flip the first zero will get the the maximum number of consecutive 1s.
    After flipping, the maximum number of consecutive 1s is 4.
```

### Note

滑动窗口，找最长包括最多k个0的窗口长度，这里k是1

两种写法，外循环分别是右边界和左边界，用左边界的时候会多算count，需要减回去并且跳出循环

类似上面那题

### Code

```java
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        int len = nums.length;
        int i = 0, count = 0;
        int res = 0;
        for (int j = 0; j < len; j++) {
            if (nums[j] == 0) {
                count++;
            }
            while (i < len && count > 1) {
                if (nums[i] == 0) {
                    count--;
                }
                i++;
            }
            res = Math.max(res, j - i + 1);
        }

        return res;
    }
}
```

```java
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        int len = nums.length;
        int j = 0, count = 0;
        int res = 0;
        for (int i = 0; i < len; i++) {
            while (j < len && count <= 1) {
                if (nums[j] == 0) {
                    count++;
                }
                if (count > 1) {
                    count--;
                    break;
                }
                j++;
            }
            if (nums[i] == 0) {
                count--;
            }
            res = Math.max(res, j - i);
        }

        return res;
    }
}
```



