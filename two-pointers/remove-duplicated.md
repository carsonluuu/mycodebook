# Remove Duplicate Numbers in Array

Given an array of integers, remove the duplicate numbers in it.

You should:

1. Do it in place in the array.
2. Move the unique numbers to the front of the array.
3. Return the total number of the unique numbers.

### Example

Given_nums_=`[1,3,1,4,4,2]`, you should:

1. Move duplicate integers to the tail of _nums_=&gt;_nums_=`[1,3,4,2,?,?]`.
2. Return the number of unique integers in _nums_=&gt;`4`.

Actually we don't care about what you place in`?`, we only care about the part which has no duplicate integers.

### Note

要先排序的。右指针遍历，左指针来判断特殊情况

一般都操作不一样的，把右指针的数换到左指针的后一位，如果所有数字都是不一样的左指针会一直比右指针慢一格，右指针会和自己换，所以也是work的。

所以最后返回就是左指针的位置加一

### Code

```java
public class Solution {
    /*
     * @param nums: an array of integers
     * @return: the number of unique integers
     */
    public int deduplication(int[] nums) {
        // write your code here
        /*
        [1,  2,  3,  4,  3,  4,  4]
                     l
                                  r
        */
        if (nums == null || nums.length == 0) {
            return 0;
        }
        Arrays.sort(nums);
        int l = 0, r = 0;
        while (r < nums.length) {
            if (nums[r] != nums[l]) {
                l++;
                nums[l] = nums[r];
            }
            r++;
        }
        return l + 1;
    }
}
```



