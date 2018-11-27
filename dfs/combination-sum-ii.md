# Combination Sum II

Given a collection of candidate numbers \(`candidates`\) and a target number \(`target`\), find all unique combinations in`candidates` where the candidate numbers sums to`target`.

Each number in`candidates` may only be used **once **in the combination.

* All numbers \(including `target`\) will be positive integers
* The solution set must not contain duplicate combinations
* May contain duplicates in input

### Examples

**Example 1:**

```
Input: candidates = [10,1,2,7,6,1,5],target = 8,
A solution set is:
[
  [1, 7],
  [1, 2, 5],
  [2, 6],
  [1, 1, 6]
]
```

**Example 2:**

```
Input: candidates = [2,5,2,1,2], target = 5,
A solution set is:
[
  [1,2,2],
  [5]
]
```

### Note

问题要求每个元素最多使用1次。index要加一，去重同全子集2

去重：`i != index && candidates[i] == candidates[i - 1]`

剪枝：`if (target < 0 ) return;`

### Code

```java
class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        List<List<Integer>> res = new ArrayList<>();
        if (candidates == null || candidates.length == 0) return res;
        Arrays.sort(candidates);
        helper(res, new ArrayList<>(), candidates, target, 0);
        return res;
    }

    private static void helper(List<List<Integer>> res, List<Integer> list, 
                               int[] candidates, int target, int index){
        if (target < 0 ) return;
        if (target == 0){
            res.add(new ArrayList(list));
            return;
        }
        for (int i = index; i < candidates.length; i++){
            if (i != index && candidates[i] == candidates[i - 1]) continue;
            list.add(candidates[i]);
            helper(res, list, candidates, target - candidates[i], i + 1);
            list.remove( list.size() - 1 );
        }
    }

}
```



