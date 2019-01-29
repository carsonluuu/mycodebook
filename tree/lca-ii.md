# Lowest Common Ancestor II

Given the root and two nodes in a Binary Tree. Find the lowest common ancestor\(LCA\) of the two nodes.

The lowest common ancestor is the node with largest depth which is the ancestor of both nodes.

The node has an extra attribute`parent`which point to the father of itself. The root's parent is null.

### Example

For the following binary tree:

```
  4
 / \
3   7
   / \
  5   6
```

LCA\(3, 5\) =`4`

LCA\(5, 6\) =`7`

LCA\(6, 7\) =`7`

### Note

变形题，现在多了一个parent指针。

可以迭代去做，**倒着循环**

5出发 5 7 4

6出发 6 7 4

最近的是7

自己也可以是自己的祖先

### Code

```java
/**
 * Definition of ParentTreeNode:
 * 
 * class ParentTreeNode {
 *     public ParentTreeNode parent, left, right;
 * }
 */


public class Solution {
    /*
     * @param root: The root of the tree
     * @param A: node in the tree
     * @param B: node in the tree
     * @return: The lowest common ancestor of A and B
     */
    public ParentTreeNode lowestCommonAncestorII(ParentTreeNode root, ParentTreeNode A, ParentTreeNode B) {
        if (root == null || root == A || root == B) {
            return root;
        }

        Set<ParentTreeNode> parentSet = new HashSet<>();
        ParentTreeNode cur = A;
        // Add node A's parent path to the pathSet
        while (cur != null) {
            parentSet.add(cur);
            cur = cur.parent;
        }
        // Traverse B's parent path, the first node that appears in A's parent path is the answer
        cur = B;
        while (cur != null) {
            if (parentSet.contains(cur)) {
                return cur;
            }
            cur = cur.parent;
        }
        return null;
    }
}
```

贴一个类似快慢指针的O\(1\)空间的做法：

p1, p2分别从A，B出发， 向root方向遍历。 p1达到root之后， 从B开始重新向root遍历。p2达到root之后， 从A开始重新向root遍历。

p1和p2在第二次遍历时，一定会在第一个intersection（i.e LCA）相遇。 时间复杂度O\(h\)，h是数的最大高度

```java
public ParentTreeNode lowestCommonAncestorII(ParentTreeNode root, ParentTreeNode A, ParentTreeNode B) {
    // write your code here
    ParentTreeNode p1 = A, p2 = B;
    while (p1 != p2) {
        p1 = p1.parent == null ? B : p1.parent;
        p2 = p2.parent == null ? A : p2.parent; 
    }
    return p1;
}
```



