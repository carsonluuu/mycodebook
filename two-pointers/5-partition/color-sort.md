# [Sort Colors](https://www.lintcode.com/problem/sort-colors/description)

Given an array with_n\_objects colored\_red_,_white\_or\_blue_, sort them so that objects of the same color are adjacent, with the colors in the order red, white and blue.

Here, we will use the integers`0`,`1`, and`2`to represent the color red, white, and blue respectively.

### Example

Given`[1, 0, 1, 2]`, sort it in-place to`[0, 1, 1, 2]`.

### Note

三个指针l, r, i

* i指针, 从左到右
* 遇到0: i和l换, 左边扩大1
* 遇到2: i和r换, 右边扩大1
* 遇到1: 接着走,不做处理

pl 和 pr 是传统的双指针，**分别代表 0~pl-1 都已经是 0 了**，**pr+1~a.length - 1 都已经是 2 了**。  
另一个角度说就是，如果你发现了一个 0 ，就可以和 pl 上的数交换，pl 就可以 ++；如果你发现了一个 2 就可以和 pr 上的数交换 pr 就可以 --。

这样，我们用第三根指针 i 来循环整个数组。如果发现 0，就丢到左边（和 pl 交换，pl++），如果发现 2，就丢到右边（和 pr 交换，pr--），如果发现 1，就不管（i++）

这就是三根指针的算法，两根指针在两边，一根指针扫描所有的数。

这里有一个实现上的小细节，当发现一个 0 丢到左边的时候，i需要++，但是发现一个2 丢到右边的时候，i不用++。原因是，**从pr 换过来的数有可能是0或者2**，需要继续判断丢到左边还是右边。**而从 pl 换过来的数，要么是0要么是1**，不需要再往右边丢了。因此这里 i 指针还有一个角度可以理解为，**i指针的左侧，都是0和1**。

### Code

```java
public class Solution {
    /**
     * @param nums: A list of integer which is 0, 1 or 2 
     * @return: nothing
     */
    public void sortColors(int[] nums) {
        // write your code here
        // [0,  0,  0,  1,  2,  2,  2]
        //              i
        //  l
        //                  r
        if (nums == null || nums.length == 0) {
            return;
        }
        int left = 0, right = nums.length - 1, i = 0;
        while (i <= right) {
            if (nums[i] == 0) {
                swap(nums, i, left);
                i++;
                left++;
            } else if (nums[i] == 2) {
                swap(nums, i, right);
                right--;
            } else {
                i++;
            }
        }
    }

    private void swap(int[] a, int i, int j) {
        int tmp = a[i];
        a[i] = a[j];
        a[j] = tmp;
    }

}
```



