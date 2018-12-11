# [Minimum Swaps To Make Sequences Increasing](https://leetcode.com/problems/minimum-swaps-to-make-sequences-increasing/description/)

We have two integer sequences`A`and`B`of the same non-zero length.

We are allowed to swap elements`A[i]`and`B[i]`.  Note that both elements are in the same index position in their respective sequences.

At the end of some number of swaps,`A`and`B`are both strictly increasing.  \(A sequence is_strictly increasing_if and only if`A[0] < A[1] < A[2] < ... < A[A.length - 1]`.\)

Given A and B, return the minimum number of swaps to make both sequences strictly increasing.  It is guaranteed that the given input always makes it possible.

### Example

```
Input:
 A = [1,3,5,4], B = [1,2,3,7]

Output:
 1

Explanation: 
Swap A[3] and B[3].  Then the sequences are:
A = [1, 3, 5, 7] and B = [1, 2, 3, 4]
which are both strictly increasing.
```

### Note

暴力做法就是DFS，也是需要掌握的，基本思路就是进行深度优先搜索去backtarcking模拟这个过程，branch factor是2。时间复杂度是O\(2^n\)，空间复杂度 O\(n\)

```
A[i] > A[i - 1] && B[i] > B[i - 1] //跳过
A[i] > B[i - 1] && B[i] > A[i - 1] //交换
```

DP做法就是针对重复子问题进行递推。这里需要一个记录两个状态换/不换的数组，因为对于递推，没有办法只根据一个状态来计算交换的数目，即不知道是交换还是保持不变得来的。

* 对于keep\[i\]: min swap for \[0:i\]
* 对于swap\[i\]: min not swap for \[0:i\]

 初始化：交换就是1，不交换就是0

* keep\[0\] = 0;
* swap\[0\] = 1;

... 2 3

... 14

会有四种

2 3      1 4      2 4      1 3

1 4      2 3      1 3      2 4

```
A[i] > A[i - 1] && B[i] > B[i - 1]
1 Good case, no swapping needed. ==>
2 Swapped A[i - 1] / B[i - 1], swap A[i], B[i] as well. ==> 
```

```
A[i] > B[i - 1] && B[i] > A[i - 1] //交换
1 A[i - 1] / B[i - 1] weren't swapped, swap for A[i] / B[i]
2 Swapped A[i - 1] / B[i - 1], no swap needed for A[i] / B[i]
```

可以使用滚动数组优化到常数时间

### Code

```java
class Solution {
    int res = Integer.MAX_VALUE;
    public int minSwap(int[] A, int[] B) {
        dfs(A, B, 0, 0);
        return res;
    }
    
    private void dfs(int[] A, int[] B, int i, int count) {
        if (count >= res) {
            return;
        }
        if (i == A.length) {
            res = Math.min(res, count);
            return;
        }
        
        if (i == 0 || A[i] > A[i - 1] && B[i] > B[i - 1]) {
            dfs(A, B, i + 1, count);
        }
        
        if (i == 0 || A[i] > B[i - 1] && B[i] > A[i - 1]) {
            swap(i, A, B);
            dfs(A, B, i + 1, count + 1);
            swap(i, A, B);
        }
    }
    
    private void swap(int i, int[] A, int[] B) {
        int temp = A[i];
        A[i] = B[i];
        B[i] = temp;
    }
}
```

```java
class Solution {
    public int minSwap(int[] A, int[] B) {
        final int len = A.length;
        int[] keep = new int[len];
        int[] swap = new int[len];
        keep[0] = 0;
        swap[0] = 1;
        for (int i = 1; i < len; i++) {
            keep[i] = len;
            swap[i] = len;
            if (A[i] > A[i - 1] && B[i] > B[i - 1]) {
                keep[i] = keep[i - 1];
                swap[i] = swap[i - 1] + 1;
            }
            if (A[i] > B[i - 1] && B[i] > A[i - 1]) {
                keep[i] = Math.min(keep[i], swap[i - 1]); // swap i - 1
                swap[i] = Math.min(swap[i], keep[i - 1] + 1); // swap i
            }
        }
        
        return Math.min(keep[len - 1], swap[len - 1]);
    }
}
```



