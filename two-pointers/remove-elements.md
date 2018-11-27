# Remove Elements

Given an array and a value, remove all occurrences of that value in place and return the new length.

The order of elements can be changed, and the elements after the new length don't matter.

### Example

Given an array`[0,4,4,0,0,2,4,4]`,`value=4`

return`4`and front four elements of the array is`[0,0,0,2]`

### Note

Two pointers.

index is the slower pointer, dealing with the duplicated cases. `nums[i] != elem` as the swap condition.

index will be the return result. 

### Code

```java
public class Solution {
    /*
     * @param A: A list of integers
     * @param elem: An integer
     * @return: The new length after remove
     */
    public int removeElement(int[] nums, int elem) {
        // write your code here
        if (nums == null || nums.length == 0) {
            return 0;
        }
        int index = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != elem) {
                nums[index] = nums[i];
                index++;
            }
        }
        
        return index;
    }
}
```



