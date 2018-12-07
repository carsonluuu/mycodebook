# Binary Tree Right Side View

Given a binary tree, imagine yourself standing on the\_right\_side of it, return the values of the nodes you can see ordered from top to bottom.

### **Example**

```
Input:
 [1,2,3,null,5,null,4]

Output:
 [1, 3, 4]

Explanation:

   1            <---
 /   \
2     3         <---
 \     \
  5     4       <---
```

### Note

层次遍历，这里最关键的一点是，最优先搞right（无论写法是递归还是迭代）

每层的第一个元素就是最右边的

### Code

```java
public List<Integer> rightSideView(TreeNode root) {
    List<Integer> res = new ArrayList<>();
    if (root == null) return res;
    helper(res, root, 0);
    return res;
}

private void helper(List<Integer> res, TreeNode root, int level) {
    if (root == null) return;
    if (res.size() == level) {
        res.add(root.val); //one at a level
    }
    helper(res, root.right, level + 1);
    helper(res, root.left , level + 1);
}
```

```java
public List<Integer> rightSideView(TreeNode root) {
    List<Integer> res = new ArrayList<>();
    if (root == null) return res;
    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);
    while (!queue.isEmpty()) {
        int size = queue.size();
        for (int i = 0; i < size; i++) { //right first
            TreeNode cur = queue.poll();
            if (i == 0) {
                res.add(cur.val);
            }
            if (cur.right != null) queue.offer(cur.right);
            if (cur.left  != null) queue.offer(cur.left );
        }
        
    }
    
    
    return res;
}
```



