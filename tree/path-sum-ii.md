# Path Sum II

You are given a binary tree in which each node contains an integer value.

Find the number of paths that sum to a given value.

The path does not need to start or end at the root or a leaf, but it must go downwards \(traveling only from parent nodes to child nodes\).

The tree has no more than 1,000 nodes and the values are in the range -1,000,000 to 1,000,000.

### **Example**

```
root = [10,5,-3,3,2,null,11,3,-2,null,1], sum = 8

      10
     /  \
    5   -3
   / \    \
  3   2   11
 / \   \
3  -2   1

Return 3. The paths that sum to 8 are:

1.  5 -> 3
2.  5 -> 2 -> 1
3. -3 -> 11
```

### Note

和之前不一样的地方在于这里没有指定起点和终点，要求给出个数

暴力做法，总数相当于是以各个节点为root，寻找个数，然后累计

最优解用到了[preSum](/data-structure/presum.md)的方法来做到线性时间，难点在于backtracking中preSum表的处理和计数

> So the idea is similar as Two sum, using HashMap to store \( key : the prefix sum, value : how many ways get to this prefix sum\) , and whenever reach a node, we check if prefix sum - target exists in hashmap or not, if it does, we added up the ways of prefix sum - target into res.
>
> For instance : in one path we have 1,2,-1,-1,2, then the prefix sum will be: 1, 3, 2, 1, 3, let's say we want to find target sum is 2, then we will have{2}, {1,2,-1}, {2,-1,-1,2} and {2}ways.

### Code

```java
//O(n^2)
class Solution {
    public int pathSum(TreeNode root, int sum) {
        if (root == null) {
            return 0;
        }

        return cointainsSum(root, sum) + 
               pathSum(root.left, sum) + pathSum(root.right, sum); 
    }

    private int cointainsSum(TreeNode root, int sum) {
        if (root == null) {
            return 0;
        }

        int res = 0;
        if (root.val == sum) {
            res++;
        }
        res += cointainsSum(root.left,  sum - root.val);
        res += cointainsSum(root.right, sum - root.val);

        return res;
    }
}
```

```java
class Solution {
    //global variable to count
    int count = 0;
    public int pathSum(TreeNode root, int sum) {
        if (root == null){
            return count;
        }
        //counting the frequency
        Map <Integer, Integer> prefixSum = new HashMap<>();
        //prefix sum[0] = 0
        prefixSum.put(0, 1);
        dfs(root, sum, prefixSum, 0);
        return count;
    }
    
    public void dfs(TreeNode root, int sum, HashMap <Integer, Integer> prefixSum, int current){
        if (root == null){
            return;
        }
        current += root.val;
        count += prefixSum.getOrDefault(current - sum, 0);
        
        prefixSum.put(current, prefixSum.getOrDefault(current, 0) + 1);
        
        dfs(root.left, sum, prefixSum, current);
        dfs(root.right, sum, prefixSum, current);
        
        //backtrack to remove the current sum
        prefixSum.put(current, prefixSum.get(current) - 1);
    }
}
```



