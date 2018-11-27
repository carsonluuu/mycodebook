# Maximum Binary Tree

Given an integer array with no duplicates. A maximum tree building on this array is defined as follow:

1. The root is the maximum number in the array.
2. The left subtree is the maximum tree constructed from left part subarray divided by the maximum number.
3. The right subtree is the maximum tree constructed from right part subarray divided by the maximum number.

Construct the maximum tree by the given array and output the root node of this tree.

### Example

```
Input: [3,2,1,6,0,5]
```

```
Output: return the tree root node representing the following tree:

      6
    /   \
   3     5
    \    / 
     2  0   
       \
        1
```

### Note

Divide and Conquer

To build the tree based on recursively finding the the max in left and right divided parts.

Mind the start and end, which suggests the ending conditions for the helper function.

### Code

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public TreeNode constructMaximumBinaryTree(int[] nums) {

        return helper(nums, 0, nums.length - 1);
    }

    private TreeNode helper(int[] nums, int start, int end) {
        if (start > end) return null;
        int index = maxIndex(nums, start, end);
        TreeNode root = new TreeNode(nums[index]);
        root.left = helper(nums, start, index - 1);
        root.right = helper(nums, index + 1, end);

        return root;
    }

    private int maxIndex(int[] nums, int start, int end) {
        int max = Integer.MIN_VALUE;
        int index = 0;
        for (int i = start; i <= end; i++) {
            if (nums[i] > max) {
                max = nums[i];
                index = i;
            }
        }
        return index;
    }
}
```



