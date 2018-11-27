Permutations II

Given a list of numbers with duplicate number in it. Find all **unique **permutations.

### Example

For numbers`[1,2,2]`the unique permutations are:

```
[
  [1,2,2],
  [2,1,2],
  [2,2,1]
]
```

### Note

和没有重复元素的 Permutation 一题相比，只加了两句话：

1. Arrays.sort\(nums\) // 排序这样所有重复的数
2. if \(i &gt; 0 && nums\[i\] == nums\[i - 1\] && !visited\[i - 1\]\) 跳过会造成重复的情况

### Code

```java
public class Solution {
    /*
     * @param nums: A list of integers.
     * @return: A list of permutations.
     */
    public List<List<Integer>> permuteUnique(int[] nums) {
        // write your code here
        List<List<Integer>> res = new ArrayList<>();
        if (nums == null) {
            return res;
        }
        Arrays.sort(nums);
        helper(nums, new boolean[nums.length], 
               new ArrayList<Integer>(), res);
        
        return res;
    }
    
    private void helper(int[] nums,
                        boolean[] visited,
                        List<Integer> list,
                        List<List<Integer>> res) {
        if (nums.length == list.size()) {
            res.add(new ArrayList<Integer>(list));
            return;
        }          
        
        for (int i = 0; i < nums.length; i++) {
            if (visited[i]) {
                continue;
            }
            //curr one the same as 
            if (i > 0 && nums[i] == nums[i - 1] && !visited[i - 1]) {
                continue;
            }
            list.add(nums[i]);
            visited[i] = true;
            helper(nums, visited, list, res);
            list.remove(list.size() - 1);
            visited[i] = false;
        }
    }
}
```



