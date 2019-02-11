# [Factor Combinations](https://leetcode.com/problems/factor-combinations/description/)

Numbers can be regarded as product of its factors. For example,

```
8 = 2 x 2 x 2;
  = 2 x 4.
```

Write a function that takes an integernand return all possible combinations of its factors.

**Note:**

1. You may assume that n is always positive.
2. Factors should be greater than 1 and less than n.

### Example

**Example 1:**

```
Input: 1
Output: []
```

**Example 2:**

```
Input: 37
Output: []
```

**Example 3:**

```
Input: 12
Output:
[
  [2, 6],
  [2, 2, 3],
  [3, 4]
]
```

**Example 4:**

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

DFS去寻找

### Code

```java
public List<List<Integer>> getFactors(int n) {
    List<List<Integer>> result = new ArrayList<List<Integer>>();
    helper(result, new ArrayList<Integer>(), n, 2);
    return result;
}

public void helper(List<List<Integer>> result, List<Integer> item, int n, int start){
    if (n <= 1) {
        if (item.size() > 1) {
            result.add(new ArrayList<Integer>(item));
        }
        return;
    }

    for (int i = start; i <= n; ++i) {
        if (n % i == 0) {
            item.add(i);
            helper(result, item, n/i, i);
            item.remove(item.size()-1);
        }
    }
}
```

```py
class Solution:
    def getFactors(self, n: 'int') -> 'List[List[int]]':
        def dfs(res, path, start, n):
            while start*start <= n:
                if n % start == 0:
                    res.append(path + [start, n//start])
                    dfs(res, path + [start], start, n//start)
                start += 1
        res = []
        dfs(res, [], 2, n)
        return res    
```



