# Unique Binary Search Trees

Given_n_, how many structurally unique **BST's **\(binary search trees\) that store values 1 ... _n_?

### **Example**

```
Input: 3

Output: 5

Explanation:

Given 
n = 3, there are a total of 5 unique BST's:

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```

### Note

The problem is to calculate the number of unique BST. To do so, we can define two functions:

1. G\(n\): the number of unique BST for a sequence of length`n`.

2. F\(i, n\): the number of unique BST, where the number`i`is served as the root of BST \(1≤i≤n\).

As we can see,

> G\(n\) is actually the desired function we need in order to solve the problem.

_Later we would see that G\(n\) can be deducted from F\(i, n\), which at the end, would recursively refers to G\(n\)._![](/assets/uniqueBST.png)  
For example,  F\(3, 7\) the number of unique BST tree with the number `3` as its root.

F\(3,7\) = G\(2\)\*G\(4\), where \[1,2\] for G\(2\) and \[4, 5, 6, 7\] for G\(4\)

F\(i, n\) = G\(i - 1\) \* G\(n - i\)

G\(n\) = ∑G\(i - 1\)\*G\(n - i\) for 1 &lt;= i &lt;= n, and G\(0\) = G\(1\) = 1

### Code





