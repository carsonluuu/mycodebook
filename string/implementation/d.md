# Find the Closest Palindrome

Given an integer n, find the closest integer \(not including itself\), which is a palindrome.

The 'closest' is defined as absolute difference minimized between two integers.

### **Example**

```
Input:
 "123"

Output:
 "121"
 
Note:
The input n is a positive integer represented by string, whose length will not exceed 18.
If there is a tie, return the smaller one as answer.
```

### Note

这道题给了我们一个数字，让我们找到其最近的回文数，而且说明了这个最近的回文数不能是其本身。比如如果给你个131，那么就需要返回121。而且返回的回文数可能位数还不同，比如当n为100的时候，我们就应该返回99，或者给了我们99时，需要返回101。那么实际上最近回文数是有范围的，比如说n为三位数，那么其最近回文数的范围在\[99, 1001\]之间，这样我们就可以根据给定数字的位数来确定出两个边界值，要和其他生成的回文数进行比较，取绝对差最小的。

下面我们来看如何求一般情况下的最近回文数，我们知道回文数就是左半边和右半边互为翻转，奇数情况下中间还有个单独的值。那么如何将一个不是回文数的数变成回文数呢，我们有两种选择，要么改变左半边，要么改变右半边。由于我们希望和原数绝对差最小，肯定是改变低位上的数比较好，所以我们改变右半边，那么改变的情况又分为两种，一种是原数本来就是回文数，这种情况下，我们需要改变中间的那个数字，要么增加1，要么减小1，比如121，可以变成111和131。另一种情况是原数不是回文数，我们只需要改变右半边就行了，比如123，变成121。那么其实这三种情况可以总结起来，分别相当于对中间的2进行了-1, +1, +0操作，那么我们就可以用一个-1到1的for循环一起处理了，先取出包括中间数的左半边，比如123就取出12，1234也取出12，然后就要根据左半边生成右半边，为了同时处理奇数和偶数的情况，我们使用一个小tricky，在反转复制左半边的时候，我们给rbegin\(\)加上len&1，当奇数时，len&1为1，这样就不会复制中间数了；为偶数时，len&1为0，这就整个翻转复制了左半边。我们把每次生成的回文串转为转为数字后加入到一个集合set中，把之前的两个边界值也同样加进去，最后我们在五个candidates中找出和原数绝对差最小的那个返回，记得别忘了在集合中删除原数，因为如果原数时回文的话, i=0时就把自己也加入集合了

### Code

```java
class Solution {
    public String nearestPalindromic(String n) {
        long len = n.length(), num = Long.valueOf(n), minDiff = Long.MAX_VALUE;
        Set<Long> set = new HashSet<>();

        set.add((long)Math.pow(10, len) + 1);
        set.add((long)Math.pow(10, len - 1) - 1);

        String left = n.substring(0, (n.length() + 1) / 2);
        long prefix = Long.valueOf(left);
        for (long i = -1; i <= 1; i++) {
            String pre = String.valueOf(prefix + i);
            String s = pre + reverseLeft(pre, len);
            set.add(Long.valueOf(s));
        }

        set.remove(num);

        long res = 0;
        for (long elem : set) {
            long diff = Math.abs(elem - num);
            if (diff < minDiff) {
                minDiff = diff;
                res = elem;
            } else if (diff == minDiff) {
                res = Math.min(res, elem);
            }
        }

        return String.valueOf(res);
    }

    private String reverseLeft(String s, long len) {
        if (len % 2 == 0) { //whole left
            return new StringBuilder(s).reverse().toString();
        } else {
            return new StringBuilder(s.substring(0, s.length() - 1)).reverse().toString();
        }
    } 
}
```



