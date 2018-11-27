# Subsets II

Given a collection of integers that might contain duplicates,_nums_, return all possible subsets \(the power set\).

Each element in a subset must be in _non-descending _order.

The ordering between two subsets is free. The solution set must not contain duplicate subsets.

### Example

Input:`[1,2,2]`  
Output:

```
[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
```

### Note

当第二次见到这个重复的元素

```
i != start && nums[i] == nums[i - 1]
```

### Code

```java
public class Solution {
    /**
     * @param nums: A set of numbers.
     * @return: A list of lists. All valid subsets.
     */
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        // write your code here
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        if (nums == null) return res;
        
        if (nums.length == 0) {
            res.add(new ArrayList<Integer>());
            return res;
        }
        Arrays.sort(nums);

        List<Integer> subset = new ArrayList<Integer>();
        helper(nums, 0, subset, res);
        
        return res;
    }
    
    private void helper(int[] nums, int start, List<Integer> list,
                        List<List<Integer>> res) {
                            
        res.add(new ArrayList<Integer>(list));
        for (int i = start; i < nums.length; i++) {
            if (i != start && nums[i] == nums[i - 1]) {
                continue;
            }
            list.add(nums[i]);
            helper(nums, i + 1, list, res);
            list.remove(list.size() - 1);
        }
    }
}
```



