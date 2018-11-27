# Most Frequent Subtree Sum

Given the root of a tree, you are asked to find the most frequent subtree sum. The subtree sum of a node is defined as the sum of all the node values formed by the subtree rooted at that node \(including the node itself\). So what is the most frequent subtree sum value? If there is a tie, return all the values with the highest frequency in any order.

### Example

Input:

```
  5
 /  \
2   -3
```

return \[2, -3, 4\], since all the values happen only once, return all of them in any order.

Input:

```
  5
 /  \
2   -5
```

return \[2\], since 2 happens twice, however -5 only occur once.

### Note

Preorder + Map

### Code

```java
class Solution {

    private int freq;
    public int[] findFrequentTreeSum(TreeNode root) {
        Map<Integer, Integer> map = new HashMap<>();

        dfs(root, map);

        List<Integer> res = new ArrayList<>();
        for (Map.Entry<Integer, Integer> e : map.entrySet()) {
            if (freq == e.getValue()) {
                res.add(e.getKey());
            }
        }

        int[] ans = new int[res.size()];
        int i = 0;
        for (int elem : res) {
            ans[i] = res.get(i);
            i++;
        }

        return ans;
    }

    private int dfs(TreeNode root, Map<Integer, Integer> map) {
        if (root == null) return 0;
        int sum = root.val + dfs(root.left, map) + dfs(root.right, map);
        map.put(sum, map.getOrDefault(sum, 0) + 1);
        freq = Math.max(freq, map.get(sum));
        return sum;
    }
}
```



