# [Tree Isomorphism Problem](https://leetcode.com/problems/flip-equivalent-binary-trees/description/)

Write a function to detect if two trees are isomorphic. Two trees are called isomorphic if one of them can be obtained from other by a series of flips, i.e. by swapping left and right children of a number of nodes.

Any number of nodes at any level can have their children swapped. Two empty trees are isomorphic.

### Example

For example, following two trees are isomorphic with following sub-trees flipped: 2 and 3, NULL and 6, 7 and 8.  
[![](https://www.geeksforgeeks.org/wp-content/uploads/ISomorphicTrees-e1368593305854.png "ISomorphicTrees")](https://www.geeksforgeeks.org/wp-content/uploads/ISomorphicTrees-e1368593305854.png)

### Note

We simultaneously traverse both trees. Let the current internal nodes of two trees being traversed be **n1 **and **n2 **respectively. There are following two conditions for subtrees rooted with n1 and n2 to be isomorphic.  
**1\) **Data of n1 and n2 is same.  
**2\) **One of the following two is true for children of n1 and n2  
……**a\) **Left child of n1 is isomorphic to left child of n2 and right child of n1 is isomorphic to right child of n2.  
……**b\) **Left child of n1 is isomorphic to right child of n2 and right child of n1 is isomorphic to left child of n2.

### Code

```java
class TreeIsomorphism 
{
    TreeNode root1, root2;

    /* Given a binary tree, print its nodes in reverse level order */
    boolean isIsomorphic(TreeNode n1, TreeNode n2) 
    {
        // Both roots are NULL, trees isomorphic by definition
        if (n1 == null && n2 == null)
            return true;

        // Exactly one of the n1 and n2 is NULL, trees not isomorphic
        if (n1 == null || n2 == null)
            return false;

        if (n1.val != n2.val)
            return false;

        return (isIsomorphic(n1.left, n2.left) && isIsomorphic(n1.right, n2.right)) || 
               (isIsomorphic(n1.left, n2.right) && isIsomorphic(n1.right, n2.left));
    }
```



