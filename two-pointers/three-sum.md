# [Three Sum](https://leetcode.com/problems/three-sum/description/)

Given an array _S \_of n integers, are there elements a_,_b_,c in S such that `a + b + c = 0`

Find all unique triplets in the array which gives the sum of zero.

### Example

For example, given array S =`{-1 0 1 2 -1 -4}`, A solution set is:

```
(-1, 0, 1)
(-1, -1, 2)
```

**Notice**

Elements in a triplet \(a,b,c\) must be in non-descending order. \(ie, a ≤ b ≤ c\)

The solution set must not contain duplicate triplets.

### Note

同向双指针，外层循环固定一个排完序的起点，内层left和right进行比较，退出条件是left &lt; right

要求不重复，需要left和right指针去重

### Code

```java
public class Solution {
    /**
     * @param numbers: Give an array numbers of n integer
     * @return: Find all unique triplets in the array which gives the sum of zero.
     */
    public List<List<Integer>> threeSum(int[] nums) {
        // write your code here
        Arrays.sort(nums);
        // -4 -1 -1 0 1 2
        List<List<Integer>> res = new ArrayList<>();
        for (int i = 0 ; i < nums.length - 2; i++) {
            if (i >= 1 && nums[i] == nums[i - 1]) {
                continue;
            }
            int left = i + 1, right = nums.length - 1, sum = 0 - nums[i];
            while (left < right) {
                if (nums[left] + nums[right] == sum) {
                    res.add(Arrays.asList(
                            nums[i], nums[left], nums[right]));
                    while (left < right && nums[left] == nums[left + 1]) {
                        left++;
                    }
                    while (left < right && nums[right] == nums[right - 1]) {
                        right--;
                    }
                    left++;
                    right--;
                }
                else if (nums[left] + nums[right] < sum) {
                    left++;
                } else {
                    right--;
                }
            }
        }
        return res;
    }
}
```



