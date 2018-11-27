# Path Sum

Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.

**Note:** A leaf is a node with no children.

**Example:**

Given the below binary tree and`sum = 22`,

```
      5
     / \
    4   8
   /   / \
  11  13  4
 /  \      \
7    2      1
```

return true, as there exist a root-to-leaf path`5->4->11->2`which sum is 22.

Find all:

```
Return:

[
   [5,4,11,2],
   [5,8,4,5]
]
```

### Note

注意要到叶子结点，添加结果的条件是最后一直减完的sum和叶子结点的大小一样，不能是`sum == 0`，因为不然递归会直接return void

或者换一种写法，最开始进行sum的减小，在增加结果的时候多进行一次backtracking（加了的都要减回来），这样是找等于0的情况。

### Code

```java
class Solution {
    public boolean hasPathSum(TreeNode root, int sum) {
        if (root == null) {
            return false;
        }
        if (root.left == null && root.right == null) {
            return sum == root.val;
        }

        return hasPathSum(root.left,  sum - root.val) ||
               hasPathSum(root.right, sum - root.val);
    }
}
```

```java
class Solution {
    public List<List<Integer>> pathSum(TreeNode root, int sum) {
        List<List<Integer>> res = new ArrayList<>();
        if (root == null) {
            return res;
        }
        helper(res, new ArrayList<>(), root, sum);
        return res;
    }

    public static void helper(List<List<Integer>> res, List<Integer> list, TreeNode root, int sum) {
        if (root == null) {
            return;
        }
        list.add(root.val);
        if (root.left == null && root.right == null) {
            if (sum - root.val == 0) {
                res.add(new ArrayList<Integer>(list));
            }
        }
        helper(res, list, root.left,  sum - root.val);
        helper(res, list, root.right, sum - root.val);
        list.remove(list.size() - 1);
    }
}
```

```java
public class Solution {
    public ArrayList<ArrayList<Integer>> pathSum(TreeNode root, int sum) {
        ArrayList<ArrayList<Integer>> rst = new ArrayList<ArrayList<Integer>>();
        ArrayList<Integer> solution = new ArrayList<Integer>();

        findSum(rst, solution, root, sum);
        return rst;
    }

    private void findSum(ArrayList<ArrayList<Integer>> result, ArrayList<Integer> solution, TreeNode root, int sum){
        if (root == null) {
            return;
        }

        sum -= root.val;

        if (root.left == null && root.right == null) {
            if (sum == 0){
                solution.add(root.val);
                result.add(new ArrayList<Integer>(solution));
                solution.remove(solution.size()-1);
            }
            return;
        }

        solution.add(root.val);
        findSum(result, solution, root.left, sum);
        findSum(result, solution, root.right, sum);
        solution.remove(solution.size()-1);
    }
}
```



