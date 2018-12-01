# [Increasing Subsequences](https://leetcode.com/problems/increasing-subsequences/description/)

Given an integer array, your task is to find all the different possible increasing subsequences of the given array, and the length of an increasing subsequence should be at least 2 .

**Note:**

1. The length of the given array will not exceed 15.
2. The range of integer in the given array is \[-100,100\].
3. The given array may contain duplicates, and two equal integers should also be considered as a special case of increasing sequence.

### **Example**

```
Input:
 [4, 6, 7, 7]

Output:
 [[4, 6], [4, 7], [4, 6, 7], [4, 6, 7, 7], [6, 7], [6, 7, 7], [7,7], [4,7,7]]
```

### Note

subset的变体

set去重，因为这里不能使用排序去重法

### Code

```java
class Solution {
    public List<List<Integer>> findSubsequences(int[] nums) {
        Set<List<Integer>> res= new HashSet<>();

        dfs(res, nums, 0, new ArrayList<>());

        return new ArrayList(res);
    }

    private void dfs(Set<List<Integer>> res, int[] nums, 
                     int start, List<Integer> list) {
        if (list.size() > 1) {
            res.add(new ArrayList<>(list));
        }

        for (int i = start; i < nums.length; i++) {
            if (list.size() == 0 || list.get(list.size() - 1) <= nums[i]) {
                list.add(nums[i]);
                dfs(res, nums, i + 1, list);
                list.remove(list.size() - 1);
            }
        }
    }
}
```



