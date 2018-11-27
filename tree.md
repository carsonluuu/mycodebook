# Tree

### **Definition for a binary tree node**

```
public class TreeNode {
     int val;
     TreeNode left;
     TreeNode right;
     TreeNode(int x) { val = x; }
}
```

### Difinition

每个节点 children = 0 / 2，为 full binary tree

![](/assets/fullTree.png)

按 level order 从左到右依次（尽量）填满，为 complete binary tree.

![](/assets/compeleteTree.png)

### **Traverse in Binary Tree **

![](/assets/tree1.png)

### **Traverse vs Divide Conquer**

1.递归是实现方式,遍历和分治是可以用递归实现的算法思想

2.Result in parameter vs Result in return value

3.Top down vs Bottom up

4.Traverse的结果要改参数,返回参数. Divide conquer的结果直接return,是个更好的接口,因为给你什么参数最好不要改.

### Recursion VS Iteration?

非递归其实是模拟递归用的stack

为什么自己模拟的可以, 调用计算机的就不行呢?

因为我们new出来的stack在heap memory里面, 能用的空间≈ memory size

stack memory ≈ process memory是计算机分给每个程序的一个很小的独占的空间,所以递归的深度太深,就不够用了

### Depth VS **Height**

树的深度是从根节点开始（其深度为1）自顶向下逐层累加的，而高度是从叶节点开始（其高度为1）自底向上逐层累加的。虽然树的深度和高度一样，但是具体到树的某个节点，其深度和高度是不一样的。我的理解是：非根非叶结点的深度是从根节点数到它的，高度是从叶节点数到它的。

```java
private int getHeight(TreeNode root) {
    if (root == null) {
        return 0;
    }
    return Math.max(getHeight(root.left), getHeight(root.right)) + 1;
}
```

```java
private int maxDepth(TreeNode root) {
    if (root == null) {
        return 0;
    }

    return 1 + Math.max(maxDepth(root.left), maxDepth(root.right));
}
```

### IS Sibling

```java
boolean isSibling(Node node, Node a, Node b) 
{ 
    // Base case 
    if (node == null) 
        return false; 

    return ((node.left == a && node.right == b) || 
            (node.left == b && node.right == a) || 
            isSibling(node.left, a, b) || 
            isSibling(node.right, a, b)); 
}
```

### Construct Binary Tree from given Parent Array

```java
/*
Input: parent[] = {1, 5, 5, 2, 2, -1, 3}
Output: root of below tree
          5
        /  \
       1    2
      /    / \
     0    3   4
         /
        6 
*/
// Creates a node with key as 'i'.  If i is root, then it changes 
    // root.  If parent of i is not created, then it creates parent first 
void createNode(int parent[], int i, Node created[])  
{ 
    // If this node is already created 
    if (created[i] != null) 
        return; 

    // Create a new node and set created[i] 
    created[i] = new Node(i); 

    // If 'i' is root, change root pointer and return 
    if (parent[i] == -1)  
    { 
        root = created[i]; 
        return; 
    } 

    // If parent is not created, then create parent first 
    if (created[parent[i]] == null) 
        createNode(parent, parent[i], created); 

    // Find parent pointer 
    Node p = created[parent[i]]; 

    // If this is first child of parent 
    if (p.left == null) 
        p.left = created[i]; 
    else // If second child 

        p.right = created[i]; 
} 

/* Creates tree from parent[0..n-1] and returns root of  
   the created tree */
Node createTree(int parent[], int n)  
{     
    // Create an array created[] to keep track 
    // of created nodes, initialize all entries 
    // as NULL 
    Node[] created = new Node[n]; 
    for (int i = 0; i < n; i++)  
        created[i] = null; 

    for (int i = 0; i < n; i++) 
        createNode(parent, i, created); 

    return root; 
}
```

### Find Level

```java
int level(Node node, Node ptr, int lev) 
{ 
    // base cases 
    if (node == null) 
        return 0; 

    if (node == ptr) 
        return lev; 

    // Return level if Node is present in left subtree 
    int l = level(node.left, ptr, lev + 1); 
    if (l != 0) 
        return l; 

    // Else search in right subtree 
    return level(node.right, ptr, lev + 1); 
}
```

### **Tree DFS creating parent \(Doubly LinkedList\)**

```java
private void dfs(TreeNode root, int target, Map<TreeNode, TreeNode> map) {
    if (root == null || root.val == target) {
        return;
    }

    if (root.left != null) {
        map.put(root.left, root);
        dfs(root.left, target, map);
    }

    if (root.right != null) {
        map.put(root.right, root);
        dfs(root.right, target, map);
    }
}

//-------------------------//
private GNode targetGNode;

private class GNode {
    TreeNode node;
    GNode parent, left, right;
    GNode (TreeNode node) {
        this.node = node;
    }
}  

private GNode cloneGraph(TreeNode node, GNode parent, TreeNode target) {
    if (node == null) return null;
    GNode gNode = new GNode(node);
    if (node == target) targetGNode = gNode;
    gNode.parent = parent;
    gNode.left = cloneGraph(node.left, gNode, target);
    gNode.right = cloneGraph(node.right, gNode, target);
    return gNode;
}
```

**Print Path between Root and Target Leaf**

```java
// A utility function that prints all nodes on the 
// path from root to target_leaf 
boolean printPath(Node node, Node target_leaf) 
{ 
    // base case 
    if (node == null) 
        return false; 

    // return true if this node is the target_leaf or 
    // target leaf is present in one of its descendants 
    if (node == target_leaf || printPath(node.left, target_leaf) 
            || printPath(node.right, target_leaf)) 
    { 
        System.out.print(node.data + " "); 
        return true; 
    } 

    return false; 
}
```



