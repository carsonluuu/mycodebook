# Binary Tree Vertical Order Traversal

Given a binary tree, return thevertical ordertraversal of its nodes' values. \(ie, from top to bottom, column by column\).

If two nodes are in the same row and column, the order should be from **left to right**.

### Example

**Examples 1:**

```
Input:
[3,9,20,null,null,15,7]

   3
  /\
 /  \
 9  20
    /\
   /  \
  15   7 

Output:
[
  [9],
  [3,15],
  [20],
  [7]
]
```

**Examples 2:**

```
Input: 
[3,9,8,4,0,1,7]

     3
    /\
   /  \
   9   8
  /\  /\
 /  \/  \
 4  01   7 

Output:
[
  [4],
  [9],
  [3,0,1],
  [8],
  [7]
]
```

**Examples 3:**

```
Input:
[3,9,8,4,0,1,7,null,null,null,2,5]
 (0's right child is 2 and 1's left child is 5)

     3
    /\
   /  \
   9   8
  /\  /\
 /  \/  \
 4  01   7
    /\
   /  \
   5   2

Output:
[
  [4],
  [9,5],
  [3,0,1],
  [8,2],
  [7]
]
```

### Note

左右孩子的index分别是父节点index减一和加一

使用TreeMap是为了维持输出的顺序，Key: Column Index, Value: List

用一个column Queue去记录当前的column index

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
    public List<List<Integer>> verticalOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        if (root == null) {
            return res;
        }
        
        Map<Integer, List<Integer>> map = new TreeMap<>();
        Queue<Integer> column = new LinkedList<>();
        Queue<TreeNode> q = new LinkedList<>();
        column.offer(0);
        q.offer(root);
        
        while (!q.isEmpty()) {
            TreeNode curr = q.poll();
            int col = column.poll();
            if (!map.containsKey(col)) {
                map.put(col, new ArrayList(Arrays.asList(curr.val)));
            } else {
                map.get(col).add(curr.val);
            }
            if (curr.left != null) {
                q.offer(curr.left);
                column.offer(col - 1);
                //min = Math.min(min, col - 1);
            }
            if (curr.right != null) {
                q.offer(curr.right);
                column.offer(col + 1);
                //max = Math.min(max, col + 1);
            }
        }
        
        for (int elem : map.keySet()) {
            res.add(map.get(elem));
        }
        
//         for (int i = min; i <= max; i++) {
//             res.add(map.get(i));
//         }
        
        return res;
    }
}
```



