# Target Sum

You are given a list of non-negative integers, a1, a2, ..., an, and a target, S. Now you have 2 symbols`+`and`-`. For each integer, you should choose one from`+`and`-`as its new symbol.

Find out how many ways to assign symbols to make sum of integers equal to target S.

### Example

```
Input: nums is [1, 1, 1, 1, 1], S is 3. 

Output: 5

Explanation:
-1+1+1+1+1 = 3
+1-1+1+1+1 = 3
+1+1-1+1+1 = 3
+1+1+1-1+1 = 3
+1+1+1+1-1 = 3

There are 5 ways to assign symbols to make the sum of nums be target 3.
```

### Note

DFS 对数组的元素进行加减，pos控制第几个元素。

记忆化递归：DFS 函数需要返回int，递归返回1或0，全局map来进行缓存，key可以是位置和当前的和

### Code

```java
class Solution {
    int count = 0;
    public int findTargetSumWays(int[] nums, int S) {
        helper(nums, 0, 0, S);

        return count;
    }

    private void helper(int[] nums, int pos, int sum, int S) {
        if (pos == nums.length) {
            if (sum == S) {
                count++;
            }    
            return;
        }

        helper(nums, pos + 1, sum - nums[pos], S);
        helper(nums, pos + 1, sum + nums[pos], S);
    }
}
```

```java
class Solution {
    HashMap<String, Integer> map;
    public int findTargetSumWays(int[] nums, int S) {
        map = new HashMap<>();

        return dfs(nums, 0, 0, S);
    }

    private int dfs(int[] nums, int pos, int sum, int S) {
        String key = pos + " " + sum;
        if (map.containsKey(key)) {
            return map.get(key);
        }

        if (pos == nums.length) {
            if (sum == S) {
                return 1;
            } else {
                return 0;
            }
        }

        int add   = dfs(nums, pos + 1, sum - nums[pos], S);
        int minus = dfs(nums, pos + 1, sum + nums[pos], S);
        int res = add + minus;
        map.put(key, res);

        return res;
    }
}
```



