# [Reverse Words in a String](https://leetcode.com/problems/reverse-words-in-a-string-ii/description/)

Given an input string, reverse the string word by word.

### **Example**

```
Input:  
["t","h","e"," ","s","k","y"," ","i","s"," ","b","l","u","e"]

Output: 
["b","l","u","e"," ","i","s"," ","s","k","y"," ","t","h","e"]
```

**Note: **

* A word is defined as a sequence of non-space characters.
* The input string does not contain leading or trailing spaces.
* The words are always separated by a single space.

**Follow up: **Could you do itin-placewithout allocating extra space?

### Note

首先把整个数组翻转， the sky is blue -&gt; eulb si yks eht  
然后根据每个空格来把每一步都翻转回来即可 -&gt; blue is sky the

时间O\(n\) 空间 O\(1\)

### Code

```java
public class Solution {
    /**
     * @param str: a string
     * @return: return a string
     */
    public char[] reverseWords(char[] str) {
        if (str == null || str.length == 0) {
            return str;
        }

        //翻转整个数组
        reverse(str, 0, str.length - 1);

        int index = 0;

        //翻转每一个单词
        for (int i = 0; i < str.length; i++) {
            if (str[i] == ' ') {
                reverse(str, index, i - 1);
                index = i + 1;
            }
        }

        //翻转最后一个单词
        reverse(str, index, str.length - 1);

        return str;
    }

    private void reverse(char[] str, int start, int end){
        while (start <= end) {
            char temp = str[start];
            str[start] = str[end];
            str[end] = temp;
            start++;
            end--;
        }
    }
}
```



