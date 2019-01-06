# Find All Duplicates in an Array

Given an array of integers, 1 ≤ a\[i\] ≤n\(n= size of array\), some elements appear **twice **and others appear **once**.

Find all the elements that appear **twice** in this array.

Could you do it without extra space and in O\(n\) runtime?

### **Example**

```
Input:
[4,3,2,7,8,2,3,1]


Output:
[2,3]
```

### Note

题目是说1-n个数字，有些重复了两次，所以有些数字就没了，我们要找出现两次的数字（们）

就是利用：

1. 非负性进行标示，修改原数组且都表示成负数，遇到负数，那么肯定说明重复了
2. 利用数字当作数组下标进行跳转

### Code

```java
class Solution {
    public List<Integer> findDuplicates(int[] nums) {
        List<Integer> res = new ArrayList<>();
        for (int num : nums) {
            int index = Math.abs(num) - 1;
            if (nums[index] < 0) {
                res.add(Math.abs(index + 1));
            }
            nums[index] = -nums[index];
        }
        
        return res;
    }
}
```



