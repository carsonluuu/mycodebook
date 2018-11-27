# [Path Sum with Digits Integers Representing](https://leetcode.com/problems/path-sum-iv/description/)

If the depth of a tree is smaller than`5`, then this tree can be represented by a list of three-digits integers.

Given a list of`ascending`three-digits integers representing a binary with the depth smaller than 5. You need to return the sum of all paths from the root towards the leaves.

**Example 1:**

```
Input: [113, 215, 221]

Output: 12

Explanation:

The tree that the list represents is:
    3
   / \
  5   1

The path sum is (3 + 5) + (3 + 1) = 12.
```

**Example 2:**

```
Input: [113, 221]

Output: 4

Explanation:

The tree that the list represents is: 
    3
     \
      1

The path sum is (3 + 1) = 4.
```

### Note

关键点是数位分离：

num / 10 is the index info with depth and pos: 10 \* depth + pos，num % 10 is value of the node

* left  = 10 \* \(depth + 1\) + 2 \* pos - 1
* right = 10 \* \(depth + 1\) + 2 \* pos

利用map存储: key is Index, val is value，dfs传入的是index信息，根据左右孩子的存在情况进行前序遍历，计算所有的路径和

时间空间都是O\(N\)

### Code

```java
class Solution {
    public int pathSum(int[] nums) {
        Map<Integer, Integer> map = new HashMap<>();
        for (int num : nums) {
            map.put(num / 10, num % 10);
        }

        int[] res = new int[1];

        dfs(nums[0] / 10, 0, res, map);

        return res[0];
    }

    private void dfs(int node, int sum, int[] res, Map<Integer, Integer> map) {
        if (!map.containsKey(node)) {
            return;
        }
        sum += map.get(node);

        int depth = node / 10;
        int pos   = node % 10;

        int left  = 10 * (depth + 1) + 2 * pos - 1;
        int right = 10 * (depth + 1) + 2 * pos;

        if (!map.containsKey(left) && !map.containsKey(right)) {
            res[0] += sum;
        } else {
            dfs(left,  sum, res, map);
            dfs(right, sum, res, map);
        }
    }
}
```



