# [Next Greater Element I](https://leetcode.com/problems/next-greater-element-i/description/)

You are given two arrays**\(without duplicates\)**`nums1`and`nums2`where`nums1`’s elements are subset of`nums2`. Find all the next greater numbers for`nums1`'s elements in the corresponding places of`nums2`.

The Next Greater Number of a number**x**in`nums1`is the first greater number to its right in`nums2`. If it does not exist, output -1 for this number.

### Example

**Example 1:**  


```
Input:
nums1 = [4,1,2], 
nums2 = [1,3,4,2].

Output:
 [-1,3,-1]

Explanation:

For number 4 in first array, you cannot find the next greater number for it in the second array,output -1.
For number 1 in first array, the next greater number for it in the second array is 3.
For number 2 in first array, there is no next greater number for it in the second array, so output -1.
```



**Example 2:**  


```
Input:
nums1 = [2,4], 
nums2 = [1,2,3,4].

Output:
 [3,-1]

Explanation:
For number 2 in the first array, the next greater number for it in the second array is 3.
For number 4 in the first array, there is no next greater number for it in the second array, so output -1.
```



###  Note

单调不严格递减栈 + Map

找到一个比栈顶大的，一直pop直到不比栈顶小，这些pop出来的下一个大的都是这个数

### Code

```java
public int[] nextGreaterElement(int[] find, int[] nums) {
    Map<Integer, Integer> map = new HashMap<>();
    Stack<Integer> stack = new Stack<>();
    for (int num : nums) {
        while (!stack.isEmpty() && stack.peek() < num) {
            map.put(stack.pop(), num);
        }
        stack.push(num);
    }
    for (int i = 0; i < find.length; i++) {
        find[i] = map.getOrDefault(find[i], -1);
    }
    return find;
}
```



