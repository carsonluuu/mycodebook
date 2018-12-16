# [Find the Duplicate Number](https://leetcode.com/problems/find-the-duplicate-number/description/)

Given an arraynumscontainingn+ 1 integers where each integer is between 1 andn\(inclusive\), prove that at least one duplicate number must exist. Assume that there is only one duplicate number, find the duplicate one.

### Example

**Example 1:**

```
Input:
[1,3,4,2,2]
Output:
 2
```

**Example 2:**

```
Input:
 [3,1,3,4,2]

Output:
 3
```

###  Note

是Set Mismatch的变种，不能改变数组

使用龟兔赛跑的快慢法吧，实在想不到。。

```
do {
tortoise = nums[tortoise];
hare = nums[nums[hare]];
} while (tortoise != hare);
```

找入口，一个指向数组起点，一个指向乌龟指针，一起走直到相遇

### Code

```java
class Solution {
    public int findDuplicate(int[] nums) {
                // Find the intersection point of the two runners.
        int tortoise = nums[0];
        int hare = nums[0];
        do {
            tortoise = nums[tortoise];
            hare = nums[nums[hare]];
        } while (tortoise != hare);

        // Find the "entrance" to the cycle.
        int ptr1 = nums[0];
        int ptr2 = tortoise;
        while (ptr1 != ptr2) {
            ptr1 = nums[ptr1];
            ptr2 = nums[ptr2];
        }
        return ptr1;
    }
}
```



