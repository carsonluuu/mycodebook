# [Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/description/)

Given an array`nums`of_n\_integers where\_n_&gt; 1,  return an array`output`such that`output[i]`is equal to the product of all the elements of`nums`except`nums[i]`.

### **Example**

```
Input:
[1,2,3,4]
Output:
[24,12,8,6]
```

**Note: **Please solve it **without division **and in O\(_n_\).

**Follow up:**  
Could you solve it with constant space complexity? \(The output array **does not **count as extra space for the purpose of space complexity analysis.\)

### Note

使用左右遍历的方法，记录left乘以right

left表示这数字左边所有数的乘积 -- 这里直接写入res数组

right表示这数字右边所有数的乘积 -- 这里使用常数迭代更新

```
Numbers: 2     3    4    5
Lefts:   1     2    2*3  2*3*4
Rights:  3*4*5 4*5  5    1
------------------------------
Result:  60    40   30  24
```

### Code

```java
class Solution {
    public int[] productExceptSelf(int[] nums) {

        int len = nums.length;
        int[] res = new int[len];
        res[0] = 1;
        for (int i = 1; i < len; i++) {
            res[i] = res[i - 1] * nums[i - 1]; 
        }
        int right = 1;
        for (int i = len - 1; i >=0; i--) {
            res[i] *= right;
            right  *= nums[i];
        }
        return res;

    }
}
```



