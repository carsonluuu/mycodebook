# [Sort Colors](https://www.lintcode.com/problem/sort-colors/description)

Given an array with_n_objects colored_red_,_white_or_blue_, sort them so that objects of the same color are adjacent, with the colors in the order red, white and blue.

Here, we will use the integers`0`,`1`, and`2`to represent the color red, white, and blue respectively.

### Example

Given`[1, 0, 1, 2]`, sort it in-place to`[0, 1, 1, 2]`.

### Note

pl 和 pr 是传统的双指针，分别代表 0~pl-1 都已经是 0 了，pr+1~a.length - 1 都已经是 2 了。  
另一个角度说就是，如果你发现了一个 0 ，就可以和 pl 上的数交换，pl 就可以 ++；如果你发现了一个 2 就可以和 pr 上的数交换 pr 就可以 --。

这样，我们用第三根指针 i 来循环整个数组。如果发现 0，就丢到左边（和 pl 交换，pl++），如果发现 2，就丢到右边（和 pr 交换，pr--），如果发现 1，就不管（i++）

这就是三根指针的算法，两根指针在两边，一根指针扫描所有的数。

这里有一个实现上的小细节，当发现一个 0 丢到左边的时候，i需要++，但是发现一个2 丢到右边的时候，i不用++。原因是，从pr 换过来的数有可能是0或者2，需要继续判断丢到左边还是右边。而从 pl 换过来的数，要么是0要么是1，不需要再往右边丢了。因此这里 i 指针还有一个角度可以理解为，i指针的左侧，都是0和1。

### Code

```java
public void sortColors(int[] a) {
    if (a == null || a.length <= 1) {
        return;
    }
    
    int pl = 0;
    int pr = a.length - 1;
    int i = 0;
    while (i <= pr) {
        if (a[i] == 0) {
            swap(a, pl, i);
            pl++;
            i++;
        } else if(a[i] == 1) {
            i++;
        } else {
            swap(a, pr, i);
            pr--;
        }
    }
}
```



