# Combination Sum III

Find all possible combinations of **k **numbers that add up to a number **n**, given that only numbers from 1 to 9 can be used and each combination should be a unique set of numbers.

* All numbers will be positive integers
* The solution set must not contain duplicate combinations.

### Example

**Example 1:**

```
Input: k = 3, n = 7

Output:
 [[1,2,4]]
```

**Example 2:**

```
Input:
k = 3, n = 9

Output:
 [[1,2,6], [1,3,5], [2,3,4]]
```

### Note

组合从n个数中选k个数，n只能是\[1, 9\]闭区间的值，起始start为1，DFS循环遍历

当k和n都为0的时候，递归退出

注意剪枝：n小于0的情况或者在循环中n小于i

### Code

```java
class Solution {
    public List<List<Integer>> combinationSum3(int k, int n) {
        List<List<Integer>> res = new ArrayList<>();
        helper(res, new ArrayList<>(), k, n, 1);
        return res;
    }
    
    private static void helper(List<List<Integer>> res, 
                               List<Integer> list, int k, 
                               int n, int start) {
        if (k == 0 && n == 0) {
            res.add(new ArrayList<>(list));
            return;
        }
        for (int i = start; i <= 9; i++) {
            if (n < i) break;
            list.add(i);
            helper(res, list, k - 1, n - i, i + 1);
            list.remove(list.size() - 1);
        }
    }
}
```



