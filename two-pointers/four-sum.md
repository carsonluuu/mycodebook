# [4 Sum](https://leetcode.com/problems/4sum/description/)

Given an array`nums`of_n\_integers and an integer_`target`_, are there elements\_a_,_b_,_c_, and_d\_in_`nums`_such that\_a_+_b_+_c_+_d_=`target`? Find all unique quadruplets in the array which gives the sum of`target`.

**Note: **The solution set must not contain duplicate quadruplets.

### **Example**

```
Given array nums = [1, 0, -1, 0, -2, 2], and target = 0.

A solution set is:
[
  [-1,  0, 0, 1],
  [-2, -1, 1, 2],
  [-2,  0, 0, 2]
]
```

### Note

主要是小优化问题

每一轮的指针都要注意去重；

* 每一轮进入内循环之前，可以直接看一眼 index 与

  * index 后面的连续几个数

  * nums\[\] 末尾的最后几个数

* 是不是会比 target 小或者大，如果 index 与后面连续的几个数加起来都没 target 大，那么检查这个 index 的必要都没有，可以直接跳过；如果 index 与最末尾的几个数相加依然小于 target，那么说明我们应该直接去看下一个更大的数当 index.

### Code

```java
public class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        List<List<Integer>> total = new ArrayList<>();
        int n = nums.length;
        if(n < 4) return total;

        Arrays.sort(nums);

        for (int i = 0; i < n - 3;i++)
        {
            if(i > 0 && nums[i] == nums[i - 1]) continue;
            if(nums[i] + nums[i + 1] + nums[i + 2] + nums[i + 3] > target) break;
            if(nums[i] + nums[n - 3] + nums[n - 2] + nums[n - 1] < target) continue;

            for (int j = i + 1; j < n - 2; j++)
            {
                if (j > i + 1 && nums[j] == nums[j - 1]) continue;
                if (nums[i] + nums[j] + nums[j + 1] + nums[j + 2] > target) break;
                if (nums[i] + nums[j] + nums[n - 2] + nums[n - 1] < target) continue;

                int left = j + 1, right = n - 1;
                while (left < right) {
                    int sum = nums[left] + nums[right] + nums[i] + nums[j];
                    if (sum < target) left++;
                    else if (sum > target) right--;
                    else {
                        total.add(Arrays.asList(nums[i],nums[j],nums[left++],nums[right--]));

                        while(left < right && nums[left] == nums[left - 1]) left ++;
                        while(left < right && nums[right] == nums[right + 1]) right --;
                    }
                }
            }
        }
        return total;
    }
}
```



