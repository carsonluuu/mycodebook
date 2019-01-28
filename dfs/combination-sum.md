# Combination Sum

Given a set of candidate numbers \(_**C**_\) and a target number \(_**T**_\), find all unique combinations in _**C **where the candidate numbers sums to _**T**.

The **same **repeated number may be chosen from **C **unlimited number of times.

* All numbers \(including `target`\) will be positive integers
* The solution set must not contain duplicate combinations
* May contain duplicates in input

### Example

**Example 1:**

```
Input:
 candidates = [2,3,6,7], target = 7

A solution set is:
[
  [7],
  [2,2,3]
]
```

**Example 2:**

```
Input: candidates = [2,3,5], target = 8

A solution set is:
[
  [2,2,2,2],
  [2,3,3],
  [3,5]
]
```

### Note

问题描述可以取一个元素重复次数

包括去重的情况（比较特殊）每层循环遇到跟前一位相同的数字（i != 0）直接跳过

```
i != 0 && candidates[i] == candidates[i - 1]
```

剪枝

```
candidates[i] > target 或 target < 0 (作为递归出口)
```

可以重复选取元素，在这种情况下index就不加一

Time: let s = target / min\(nums\[i\]\) T = C\(s,1\) + C\(s, 2\) + ... + C\(s, s\) = 2^s

Space: O\(target / min\(nums\[i\]\) \)

### Code

```java
public class Solution {
    public  List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> result = new ArrayList<>();
        if (candidates == null) {
            return result;
        }

        List<Integer> combination = new ArrayList<>();
        Arrays.sort(candidates);

        helper(candidates, 0, target, combination, result);

        return result;
    }

     private void helper(int[] candidates, int index, int target,
                         List<Integer> combination, List<List<Integer>> result) {
        if (target == 0) {
            result.add(new ArrayList<Integer>(combination));
            return;
        }

        for (int i = index; i < candidates.length; i++) {
            if (candidates[i] > target) {
                break;
            }

            if (i != 0 && candidates[i] == candidates[i - 1]) {
                continue;
            }

            combination.add(candidates[i]);
            helper(candidates, i, target - candidates[i], combination, result);
            combination.remove(combination.size() - 1);
        }
    }
}
```



