# All Nodes Distance K in Binary Tree

We are given a binary tree \(with root node `root`\), a`target`node, and an integer value`K`.

Return a list of the values of all nodes that have a distance`K`from the`target`node.  The answer can be returned in any order.

### **Example**

```
Input: root = [3,5,1,6,2,0,8,null,null,7,4], target = 5, K = 2

Output: [7,4,1]

Explanation: 
The nodes that are a distance 2 from the target node (with value 5)
have values 7, 4, and 1.
```

![](/assets/k-distance-tree.png)

### Note

dfs -&gt; back edge map

bfs -&gt; two way level order

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
    public List<Integer> distanceK(TreeNode root, TreeNode target, int k) {
        Map<TreeNode, TreeNode> map = new HashMap<>();

        dfs(root, target.val, map);

        List<Integer> res = bfs(target, map, k);

        return res;
    }

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

    private List<Integer> bfs(TreeNode node, Map<TreeNode, TreeNode> map, int k) {
        Queue<TreeNode> q = new LinkedList<>();
        Set<TreeNode> set = new HashSet<>();

        List<Integer> res = new ArrayList<>();

        q.offer(node);
        set.add(node);
        while (!q.isEmpty() && k >= 0) {
            int size = q.size();
            for (int i = 0; i < size; i++) {
                TreeNode curr = q.poll();
                if (k == 0) {
                    res.add(curr.val);
                }
                if (curr.left != null && set.add(curr.left)) {
                    q.offer(curr.left);
                }
                if (curr.right != null && set.add(curr.right)) {
                    q.offer(curr.right);
                }     
                if (map.containsKey(curr) && set.add(map.get(curr))) {
                    q.offer(map.get(curr));
                }
            }
            k--;
        }

        return res;
    }
}
```

```java
class Solution {
   Map<TreeNode, List<TreeNode>> map = new HashMap();
   public List<Integer> distanceK(TreeNode root, TreeNode target, int K) {
         List<Integer> res = new ArrayList<Integer> ();
        if (root == null || K < 0) return res;
        buildMap(root, null); 
        if (!map.containsKey(target)) return res;
        Set<TreeNode> visited = new HashSet<TreeNode>();
        Queue<TreeNode> q = new LinkedList<TreeNode>();
        q.add(target);
        visited.add(target);
        while (!q.isEmpty()) {
            int size = q.size();
            if (K == 0) {
                for (int i = 0; i < size ; i++) res.add(q.poll().val);
                return res;
            }
            for (int i = 0; i < size; i++) {
                TreeNode node = q.poll();
                for (TreeNode next : map.get(node)) {
                    if (visited.contains(next)) continue;
                    visited.add(next);
                    q.add(next);
                }
            }
            K--;
        }
        return res;
    }
    //graph-like building
    private void buildMap(TreeNode node, TreeNode parent) {
        if (node == null) return;
        if (!map.containsKey(node)) {
            map.put(node, new ArrayList<TreeNode>());
            if (parent != null)  { map.get(node).add(parent); map.get(parent).add(node) ; }
            buildMap(node.left, node);
            buildMap(node.right, node);
        }
    }    
}
```



