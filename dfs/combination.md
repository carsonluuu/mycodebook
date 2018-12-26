# Combination

Given two integers _n \_and \_k_, return all possible combinations of _k \_numbers out of 1 ... \_n_.

### Example

```
Input:
 n = 4, k = 2

Output:
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```

### Note

递归出口：k减到0

start从1开始

Time: O\(n^min\(k, n - k\)\)

Space: O\(n\)

### Code

```java
class Solution {
    public List<List<Integer>> combine(int n, int k) {
        List<List<Integer>> res = new ArrayList<>();
        if (k <= 0 || n <= 0 || n < k) return res;
        helper(res, new ArrayList(), n, k, 1); //index starts from 1;
        return res;
    }

    private static void helper(List<List<Integer>> res, 
                               List<Integer> list, int n, int k, int index) {
        if (k == 0) {
            res.add(new ArrayList<>(list));
            return;
        }

        for (int i = index; i <= n; i++) {
            list.add(i);
            helper(res, list, n, k - 1, i + 1);
            list.remove(list.size() - 1);
        }
    }

}
```



