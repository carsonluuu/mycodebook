# [Three Sum With Multiplicity](https://leetcode.com/problems/3sum-with-multiplicity/description/)

Given an integer array`A`, and an integer`target`, return the number of tuples `i, j, k`  such that`i < j < k`and `A[i] + A[j] + A[k] == target`.

**As the answer can be very large, return it modulo **`10^9 + 7`.

### Example

**Example 1:**

```
Input: 
A = 
[1,1,2,2,3,3,4,4,5,5]
, target = 
8
Output: 
20
Explanation: 

Enumerating by the values (A[i], A[j], A[k]):
(1, 2, 5) occurs 8 times;
(1, 3, 4) occurs 8 times;
(2, 2, 4) occurs 2 times;
(2, 3, 3) occurs 2 times.
```

**Example 2:**

```
Input: 
A = 
[1,1,2,2,2,2]
, target = 
5
Output: 
12
Explanation: 

A[i] = 1, A[j] = A[k] = 2 occurs 12 times:
We choose one 1 from [1,1] in 2 ways,
and two 2s from [2,2,2,2] in 6 ways.
```

```
Note:
    3 <= A.length <= 3000
    0 <= A[i] <= 100
    0 <= target <= 300
```

### Note

1. 现在可以取重复数了，左右指针相等情况就是C\(right - left + 1, 2\)，左右指针去重时，要记录一下重复的个数，其结果需要相乘
2. Map做法，使用了额外空间，稍微会快一滴滴，没有方法1的排序过程
3. 背包做法，伪多项式时间了，不是特别推荐

### Code

```java
class Solution {
    public int threeSumMulti(int[] A, int target) {
        Arrays.sort(A);
        long res = 0l;
        int len = A.length;
        for (int i = 0; i < len - 2; i++) {
            int left = i + 1, right = len - 1;
            int sum = target - A[i];
            while (left < right) {
                if (A[left] + A[right] < sum) {
                    left++;
                } else if (A[left] + A[right] > sum) {
                    right--;
                } else {
                    if (A[left] == A[right]) {
                        res += (right - left + 1) * (right - left) / 2;
                        break;
                    }
                    int l = 1, r = 1;
                    while (left + l < right && A[left + l] == A[left]) {
                        l++;
                    }
                    while (left < right - r && A[right - r] == A[right]) {
                        r++;
                    }
                    res += l*r;
                    left  += l;
                    right -= r;
                }
            }
        }

        return (int)(res % (1e9 + 7));
    }
}
```

```java
class Solution {
    public int threeSumMulti(int[] A, int target) {
        Map<Integer, Integer> map = new HashMap<>();
        long res = 0;
        for (int i = 0; i < A.length; i++) {
            res += map.getOrDefault(target - A[i], 0);

            for (int j = 0; j < i; j++) {
                int temp = A[i] + A[j];
                map.put(temp, map.getOrDefault(temp, 0) + 1);
            }
        }
        return res;
    }
}
```



