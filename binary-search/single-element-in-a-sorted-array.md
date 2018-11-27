# [Single Element in a Sorted Array](https://leetcode.com/problems/single-element-in-a-sorted-array/description/)

Given a sorted array consisting of only integers where every element appears twice except for one element which appears once. Find this single element that appears only once.

**Example 1:**

```
Input: [1,1,2,3,3,4,4,8,8]
Output: 2
```

**Example 2:**

```
Input: [3,3,7,7,10,11,11]
Output: 10
```

### Note

jiuzhang的模版有些小问题，主要是三个元素的情况，这里终点取长度减一，防一波越界

```
[1,1,2]
[0,1,1]
```

### Code

```java
class Solution {
    public int singleNonDuplicate(int[] nums) {
        int start = 0, end = nums.length - 1;
        while (start < end) {
            int mid = (end - start) / 2 + start;
            if (nums[mid - 1] != nums[mid] && nums[mid] != nums[mid + 1]) {
                return nums[mid];
            } else if (nums[mid - 1] == nums[mid] && mid % 2 == 1) {
                start = mid + 1;
            } else if (nums[mid] == nums[mid + 1] && mid % 2 == 0) {
                start = mid + 1;
            } else {
                end = mid - 1;
            }
        }

        return nums[end];
    }
}
```



