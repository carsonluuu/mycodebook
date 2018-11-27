# Factor Combinations

Numbers can be regarded as product of its factors. For example,

```
8 = 2 x 2 x 2;
  = 2 x 4.
```

Write a function that takes an integernand return all possible combinations of its factors.

### Example

**Example 1:**

```
Input: 1
Output: []
```

**Example 2:**

```
Input: 37
Output: []
```

**Example 3:**

```
Input: 12
Output:
[
  [2, 6],
  [2, 2, 3],
  [3, 4]
]
```

**Example 4:**

```
Input: 32
Output:
[
  [2, 16],
  [2, 2, 8],
  [2, 2, 2, 4],
  [2, 2, 2, 2, 2],
  [2, 4, 4],
  [4, 8]
]
```

### Note

循环保证结果是递增序列

index从2开始

递归出口是n为1并且结果的长度比1大（包括至少两个元素）

条件：能整除，DFS传递其商

### Code

```java
class Solution {
    public List<List<Integer>> getFactors(int n) {
        List<List<Integer>> res = new ArrayList<>();
        if (n == 1) return res;
        helper(res, new ArrayList<>(), n, 2);
        return res;
    }
    private static void helper(List<List<Integer>> res, 
                               List<Integer> list, 
                               int n, int index) {
        if (n == 1 && list.size() > 1) {
            res.add(new ArrayList<>(list));
            return;
        }
        for (int i = index; i <= n; i++) {
            if (n % i == 0) {
                list.add(i);
                helper(res, list, n/i, i);
                list.remove(list.size() - 1);   
            }            
        }
    }
}
```



