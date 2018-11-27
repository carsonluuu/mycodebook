# [Permutation Sequence](https://leetcode.com/problems/permutation-sequence/description/)

给定 _n _和 _k_，求`123..n`组成的排列中的第_k_个排列

By listing and labeling all of the permutations in order,

We get the following sequence \(ie, for n = 3\):

1. "123"

2. "132"

3. "213"

4. "231"

5. "312"

6. "321"

Given n and k, return the kth permutation sequence.

Note: Given n will be between 1 and 9 inclusive.

### Example

**Example 1:**

```
Input:
 n = 3, k = 3

Output:
 "213"
```

**Example 2:**

```
Input:
 n = 4, k = 9

Output:
 "2314"
```

### Note

To be revisited...

### Code

```java
public class Solution {

    public String getPermutation(int n, int k) {
        StringBuilder sb = new StringBuilder();
        boolean[] used = new boolean[n];

        k = k - 1;
        int factor = 1;
        for (int i = 1; i < n; i++) {
            factor *= i;
        }

        for (int i = 0; i < n; i++) {
            int index = k / factor;
            k = k % factor;
            for (int j = 0; j < n; j++) {
                if (used[j] == false) {
                    if (index == 0) {
                        used[j] = true;
                        sb.append((char) ('0' + j + 1));
                        break;
                    } else {
                        index--;
                    }
                }
            }
            if (i < n - 1) {
                factor = factor / (n - 1 - i);
            }
        }

        return sb.toString();
    }
}
```



