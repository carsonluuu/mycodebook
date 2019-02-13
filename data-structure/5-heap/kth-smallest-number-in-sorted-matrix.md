# [Kth Smallest Number in Sorted Matrix](https://www.lintcode.com/problem/kth-smallest-number-in-sorted-matrix/description)

Find the _k_th smallest number in a row and column sorted matrix.

Each row and each column of the matrix is incremental.

### Example

**Example 1:**

```
Input:
[
  [1 ,5 ,7],
  [3 ,7 ,8],
  [4 ,8 ,9],
]
k = 4
Output: 5

```

**Example 2:**

```
Input:
[
  [1, 2],
  [3, 4]
]
k = 3
Output: 3
```

### Note

其实是利用优先级队列做BFS，搜索直到第k小，对于

```
[
  [1 ,5 ,7],
  [3 ,7 ,8],
  [4 ,8 ,9],
]
```

1是第一层，斜着的3，5是第二层，再斜着的4，7，7是第三层，8，8是第四层, 9是最后一层。  
利用方向数组进行向下和向右搜索，利用visited数组记录访问过的位置（可以用hashset,如x\*103 + y），minheap移除的都是较小的那个。  
Time Complexity: O\(klog\(min\(m,n,k\)\)\)，队列最大长度是最长的那个对角线的元素个数，which is 行和列长度的更小者（如：很高或者很宽的矩阵）；还有一点是当k比行和列长度的更小者小时，队列的最大长度其实是k。  
Space Complexity: O\(min\(m,n,k\) + mn\)，visited数组和pq的大小

### Code

```java
public class Solution {
    /**
     * @param matrix: a matrix of integers
     * @param k: An integer
     * @return: the kth smallest number in the matrix
     */
    private static class Node {
        int x, y, val;
        public Node(int x, int y, int val) {
            this.x = x;
            this.y = y;
            this.val = val;
        }
    }
    
    private final int[][] DIR = new int[][]{{1, 0}, {0, 1}}; 
    
    public int kthSmallest(int[][] matrix, int k) {
        // write your code here
        if (matrix == null || matrix.length == 0 || 
            matrix[0] == null || matrix[0].length == 0 || k <= 0) {
            throw new IllegalArgumentException();     
        }
        
        int m = matrix.length, n = matrix[0].length;
        boolean[][] visited = new boolean[m][n];
        Queue<Node> pq = new PriorityQueue<>((a,b) -> a.val - b.val);
        pq.offer(new Node(0, 0, matrix[0][0]));
        
        for (int i = 0; i < k - 1; i++) {
            Node curr = pq.poll();
            for (int dir = 0; dir < 2; dir++) {
                int x = curr.x + DIR[dir][0];
                int y = curr.y + DIR[dir][1];
                if (x < m && y < n && !visited[x][y]) {
                    visited[x][y] = true;
                    pq.offer(new Node(x, y, matrix[x][y]));
                }
            }
        }
        
        return pq.poll().val;
    }
}
```



