# Find Minimum in Rotated Sorted Array

Suppose a sorted array is rotated at some pivot unknown to you beforehand.

\(i.e.,`0 1 2 4 5 6 7`might become`4 5 6 7 0 1 2`\).

Find the minimum element.

### Example

Given`[4, 5, 6, 7, 0, 1, 2]`return`0`

### Note1

![](/assets/sortedRotatedArray.png)

就是在两段上升区间, 找到第一个"x"，肯定是在右半边

可以定位最后一个元素：**小于等于**它时不断更新end为mid，否则一直向右找

也可以不定位，直接使用end作为比较的对象，因为它是确保递增的，这半部分右边比左边大

### Code1

```java
public class Solution {
    /**
     * @param nums: a rotated sorted array
     * @return: the minimum number in the array
     */
    public int findMin(int[] nums) {
        // write your code here
        if (nums == null || nums.length == 0) {
            return -1;
        }
        int start = 0, end = nums.length - 1;
        int target = nums[nums.length - 1];
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (nums[mid] <= target) {
                end = mid;
            } else {
                start = mid;
            }
        }
        if (nums[start] <= target) {
            return nums[start];
        } else {
            return nums[end];
        }
    }
}
```

### Note2

如果有重复：

nums\[mid\] == nums\[end\], then we should enclose the end by end--, to throw the boundary away

### Code2

```java
public class Solution {
    /**
     * @param nums: a rotated sorted array
     * @return: the minimum number in the array
     */
    public int findMin(int[] nums) {
        // write your code here
        if (nums == null || nums.length == 0) {
            return -1;
        }

        int start = 0, end = nums.length - 1;
        while (start + 1 < end) {
            int mid = (end - start) / 2 + start;
            if (nums[mid] == nums[end]) {
                end--;
            } else if (nums[mid] < nums[end]) {
                end = mid; 
            } else {
                start = mid;
            }
        }

        if (nums[start] <= nums[end]) {
            return nums[start];
        }
        return nums[end];

    }
}
```



