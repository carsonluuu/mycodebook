# [Triangle Count](http://www.lintcode.com/en/problem/triangle-count/)

Given an array of integers, how many three numbers can be found in the array, so that we can build an triangle whose three edges length is the three numbers that we find?

### Example

Given array S =`[3,4,6,7]`, return`3`. They are:

```
[3,4,6]
[3,6,7]
[4,6,7]

```

Given array S =`[4,4,4,4]`, return`4`. They are:

```
[4(1),4(2),4(3)]
[4(1),4(2),4(4)]
[4(1),4(3),4(4)]
[4(2),4(3),4(4)]
```

### Note



### Code

```java
public class Solution {
    /**
     * @param nums: A list of integers
     * @return: An integer
     */
    public int triangleCount(int[] nums) {
        // write your code here
        if (nums == null || nums.length < 3) {
            return 0;
        }
        Arrays.sort(nums);
        int res = 0;
        // 3 4 6 7 8
        //         i
        // l     r
        for (int i = 2; i < nums.length; i++) {
            int left = 0;
            int right = i - 1;
            while (left < right) {
                if (nums[left] + nums[right] > nums[i]) {
                    res += right - left;
                    right--;
                } else {
                    left++;
                }
            }
        }
        return res;
    }
}
```



