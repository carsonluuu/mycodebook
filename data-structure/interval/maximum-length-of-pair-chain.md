# Maximum Length of Pair Chain

You are given`n`pairs of numbers. In every pair, the first number is always smaller than the second number.

Now, we define a pair`(c, d)`can follow another pair`(a, b)`if and only if`b < c`. Chain of pairs can be formed in this fashion.

Given a set of pairs, find the length longest chain which can be formed. You needn't use up all the given pairs. You can select pairs in any order.

### Example

```
Input:
[[1,2], [2,3], [3,4]]

Output:
2

Explanation:
The longest chain is [1,2] -> [3,4]
```

### Note

类似Non-overlapping，这里的重合条件是小于等于，每有一个满足条件就将它从原长度中删去。

### Code

```java
class Solution {
    public int findLongestChain(int[][] pairs) {
        Arrays.sort(pairs, (a, b) -> a[0] - b[0]);
        int res = pairs.length;
        int last = 0;
        for (int i = 1; i < pairs.length; i++) {
            if (pairs[i][0] <= pairs[last][1]) {
                res--;
                if (pairs[i][1] <= pairs[last][1]) {
                    last = i;
                }
            } else {
                last = i;
            }
        }

        return res;
    }
}
```



