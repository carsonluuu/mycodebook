# [Next Greater Element II](https://leetcode.com/problems/next-greater-element-ii/description/)

Given a circular array \(the next element of the last element is the first element of the array\), print the Next Greater Number for every element. The Next Greater Number of a number x is the first greater number to its traversing-order next in the array, which means you could search circularly to find its next greater number. If it doesn't exist, output -1 for this number.

### **Example**

```
Input:
 [1,2,1]

Output:
 [2,-1,2]

Explanation:
 The first 1's next greater number is 2; 


The number 2 can't find next greater number; 

The second 1's next greater number needs to search circularly, which is also 2
```

### Note

环形版本，就是在两倍长度的数组上重复之前那题

### Code

```java
class Solution {
    public int[] nextGreaterElements(int[] nums) {
        int[] res = new int[nums.length];
        Stack<Integer> stack = new Stack<>();
        Arrays.fill(res, -1);
        int len = nums.length;
        for (int i = 0; i < 2 * len; i++) {
            int num = nums[i % len];
            while (!stack.isEmpty() && nums[stack.peek()] < num) {
                res[stack.pop()] = num; 
            }
            if (i < len) {
                stack.push(i);
            }
        }
        return res;
    }
}
```





