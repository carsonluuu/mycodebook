### Definition

```

```

### Pre-Order

Recursion

```java
class Solution {
    public List<Integer> preorder(Node root) {
        List<Integer> res = new ArrayList<>();

        dfs(res, root);

        return res;
    }

    private void dfs(List<Integer> res, Node root) {
        if (root == null) {
            return;
        }

        res.add(root.val);
        for (Node nei : root.children) {
            dfs(res, nei);
        }
    }
}
```

Iterative

```java
class Solution {
    public List<Integer> preorder(Node root) {
        List<Integer> list = new ArrayList<>();
        if (root == null) return list;

        Stack<Node> stack = new Stack<>();
        stack.add(root);

        while (!stack.empty()) {
            root = stack.pop();
            list.add(root.val);
            for (int i = root.children.size() - 1; i >= 0; i--)
                stack.add(root.children.get(i));
        }

        return list;
    }
}
```

### Post-Order

Recursion

```java
class Solution {
    public List<Integer> postorder(Node root) {
        List<Integer> res = new ArrayList<>();

        dfs(res, root);

        return res;
    }

    private void dfs(List<Integer> res, Node root) {
        if (root == null) {
            return;
        }

        for (Node nei : root.children) {
            dfs(res, nei);
        }

        res.add(root.val);
    }
}
```

Iterative

```java
class Solution {
    public List<Integer> postorder(Node root) {
        List<Integer> list = new ArrayList<>();
        if (root == null) return list;

        Stack<Node> stack = new Stack<>();
        stack.add(root);

        while(!stack.isEmpty()) {
            root = stack.pop();
            list.add(root.val);
            for(Node node: root.children)
                stack.add(node);
        }
        Collections.reverse(list);
        return list;
    }
}
```

### Level-Order

Recursion

```java
class Solution {
    public List<List<Integer>> levelOrder(Node root) {
        return levelOrder(root, 0, new ArrayList<>());
    }

    private List<List<Integer>> levelOrder(Node root, int level, List<List<Integer>> res){
        if (root == null){
            return res;
        }
        if (level == res.size()) {
            res.add(new ArrayList<>());
        }

        res.get(level).add(root.val);

        for (Node n : root.children){
            levelOrder(n, level + 1, res);
        }
        return res;
    }
}
```

Iterative

```java
class Solution {
    public List<List<Integer>> levelOrder(Node root) {
        List<List<Integer>> res = new LinkedList<>();

        if (root == null) return res;

        Queue<Node> queue = new LinkedList<>();

        queue.offer(root);

        while (!queue.isEmpty()) {
            List<Integer> currLevel = new LinkedList<>();
            int len = queue.size();
            for (int i = 0; i < len; i++) {
                Node curr = queue.poll();
                currLevel.add(curr.val);
                for (Node c : curr.children) {
                    queue.offer(c);
                }
            }
            res.add(currLevel);
        }

        return res;
    }
}
```

### Max Depth

```java
class Solution {
    public int maxDepth(Node root) {
        if (root == null) {
            return 0;
        }

        int max = 0;
        for (Node child : root.children) {
            int depth = maxDepth(child);
            max = Math.max(max, depth);
        }
        return max + 1;
    }
}
```



