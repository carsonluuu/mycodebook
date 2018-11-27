# Sort Colors II

Given an array of_n_objects with_k_different colors \(numbered from 1 to k\), sort them so that objects of the same color are adjacent, with the colors in the order 1, 2, ... k.

### Example

Given colors=`[3, 2, 2, 1, 4]`,`k=4`, your code should sort colors in-place to`[1, 2, 2, 3, 4]`.

### Note

### 

### Code

```java
public class Solution {
    /**
     * @param colors: A list of integer
     * @param k: An integer
     * @return: nothing
     */
    public void sortColors2(int[] colors, int k) {
        // write your code here
        if (colors == null || colors.length == 0) {
            return ;
        }
        rainbowSort(colors, 0, colors.length - 1, 1, k);
    }
    
    private static void rainbowSort(int[] colors,
                                    int left,
                                    int right,
                                    int colorFrom,
                                    int colorTo) {
        if (colorFrom == colorTo) {
            return ;
        }                       
        if (left >= right) {
            return ;
        }
        
        int colorMid = (colorFrom + colorTo) / 2;
        int l = left, r = right;
        while (l <= r) {
            while (l <= r && colors[l] <= colorMid) {
                l++;
            }
            while (l <= r && colors[r] > colorMid) {
                r--;
            }
            if (l <= r) {
                int temp = colors[l];
                colors[l++] = colors[r];
                colors[r--] = temp;
            }
        }
        rainbowSort(colors, left, r, colorFrom, colorMid);
        rainbowSort(colors, l, right, colorMid + 1, colorTo);

    }
    
}
```



