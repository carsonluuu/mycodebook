# [Serialize and Deserialize Binary Tree](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/description/)

Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.

### Note

* #### If given Tree is Binary Search Tree? {#if-given-tree-is-binary-search-tree}

  If the given Binary Tree is Binary Search Tree, we can store it by either storing preorder or postorder traversal. In case of Binary Search Trees, only preorder or postorder traversal is sufficient to store structure information.

* #### If given Binary Tree is Complete Tree? {#if-given-binary-tree-is-complete-tree}

  A Binary Tree is complete if all levels are completely filled except possibly the last level and all nodes of last level are as left as possible \(Binary Heaps are complete Binary Tree\). For a complete Binary Tree, level order traversal is sufficient to store the tree. We know that the first node is root, next two nodes are nodes of next level, next four nodes are nodes of 2nd level and so on.

* #### If given Binary Tree is Full Tree? {#if-given-binary-tree-is-full-tree}

  A full Binary is a Binary Tree where every node has either 0 or 2 children. It is easy to serialize such trees as every internal node has 2 children. We can simply store preorder traversal and store a bit with every node to indicate whether the node is an internal node or a leaf node.

* #### How to store a general Binary Tree? {#how-to-store-a-general-binary-tree}

  A simple solution is to store both Inorder and Preorder traversals. This solution requires requires space twice the size of Binary Tree. We can save space by storing Preorder traversal and a marker for NULL pointers.

#### 解决这题的关键就是，自己补位，构建一个 full binary tree 出来。 {#解决这题的关键就是，自己补位，构建一个-full-binary-tree-出来。}

### Option One - Preorder

```
We may serialize the following tree:

    1
   / \
  2   3
     / \
    4   5

as "1,2,#,#,3,4,#,#,5,#,#"
```

```java
public class Codec {
    private static final String NULL = "#";
    private static final String SEP = ",";

    public String serialize(TreeNode root) {
        if (root == null) {
            return "";
        }
    
        StringBuilder sb = new StringBuilder();
        // PreOrder traversal
        Stack<TreeNode> s = new Stack<>();
        s.push(root);
        while (!s.isEmpty()) {
            TreeNode cur = s.pop();
            if (cur == null) {
                sb.append(NULL).append(SEP);
                continue;
            }
            sb.append(cur.val).append(SEP);
            s.push(cur.right);
            s.push(cur.left);
        }
    
        sb.setLength(sb.length() - 1);
        //System.out.print(sb.toString());
        return sb.toString();
    }

    public TreeNode deserialize(String data) {
        if (data == null || data.length() == 0) {
            return null;
        }

        StringTokenizer st = new StringTokenizer(data, SEP);
        return deseriaHelper(st);
    }

    private TreeNode deseriaHelper(StringTokenizer st) {
        if (!st.hasMoreTokens()) {
            return null;
        }

        String val = st.nextToken();
        if (val.equals(NULL)) {
            return null;
        }
    
        TreeNode root = new TreeNode(Integer.parseInt(val));
        root.left = deseriaHelper(st);
        root.right = deseriaHelper(st);
    
        return root;
    }
}
```

### Option Two - Level order

```
We may serialize the following tree:

    1
   / \
  2   3
     / \
    4   5

as "{1,2,3,#,#,4,5}"
```

```java
public class Codec {
    public String serialize(TreeNode root) {
        StringBuilder sb = new StringBuilder();
        sb.append("{");

        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);
        while (!q.isEmpty()) {
            TreeNode curr = q.poll();
            if (curr == null) {
                sb.append("#");
            } else {
                q.offer(curr.left);
                q.offer(curr.right);
                sb.append(curr.val);
            }
            sb.append(",");
        }

        for (int i = sb.length() - 1; i >= 0; i--) {
            if (sb.charAt(i) == '#' || sb.charAt(i) == ',') {
                sb.deleteCharAt(i);
            } else {
                break;
            }
        }

        sb.append("}");
        System.out.print(sb.toString());
        return sb.toString(); 
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        if (data.equals("{}")) {
            return null;
        }

        String[] vals = data.substring(1, data.length() - 1).split(",");
        List<TreeNode> list = new ArrayList<>();
        TreeNode root = new TreeNode(Integer.parseInt(vals[0]));
        list.add(root);

        boolean flag = true;
        int index = 0;
        for (int i = 1; i < vals.length; i++) {
            if (!vals[i].equals("#")) {
                TreeNode node = new TreeNode(Integer.parseInt(vals[i]));
                if (flag) {
                    list.get(index).left = node;
                } else {
                    list.get(index).right = node;
                }
                list.add(node);
            }
            if (!flag) {
                index++;
            }
            flag = !flag;
        }

        return root;
    }
}
```



