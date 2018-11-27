# [4 Sum](https://leetcode.com/problems/4sum/description/)

Given an array`nums`of_n_integers and an integer`target`, are there elements_a_,_b_,_c_, and_d_in`nums`such that_a_+_b_+_c_+_d_=`target`? Find all unique quadruplets in the array which gives the sum of`target`.

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

### Code

```java
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        List<List<Integer>> res = new ArrayList<> ();
        if(nums.length < 4) return res;
        Arrays.sort(nums);
        for (int i = 0; i < nums.length - 3; i++){
            if(i > 0 && nums[i] == nums[i - 1]) continue;
            for(int j = i + 1; j < nums.length - 2; j++){
                if(j > i + 1 && nums[j] == nums[j - 1]) continue;
                int low = j + 1, high = nums.length - 1;
                while(low < high){
                    if (target == nums[i] + nums[j] + nums[low] + nums[high]){
                        res.add(Arrays.asList(nums[i], nums[j], nums[low], nums[high]));
                        while(low < high && nums[low] == nums[low + 1]) low++;
                        while(low < high && nums[high] == nums[high - 1]) high--;
                        low++; high--;
                    }
                    else if(target > nums[i] + nums[j] + nums[low] + nums[high]) low++;
                    else high--;
                }
            }
        }
        return res;
        
    }
}
```



