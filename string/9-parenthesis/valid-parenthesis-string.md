# [Valid Parenthesis String](https://leetcode.com/problems/valid-parenthesis-string/description/)

Given a string containing only three types of characters: '\(', '\)' and '\*', write a function to check whether this string is valid. We define the validity of a string by these rules:

1. Any left parenthesis `'('`must have a corresponding right parenthesis`')'`.
2. Any right parenthesis`')'`must have a corresponding left parenthesis`'('`.
3. Left parenthesis`'('`must go before the corresponding right parenthesis`')'`.
4. `'*'`could be treated as a single right parenthesis`')'`or a single left parenthesis`'('`or an empty string.
5. An empty string is also valid.

### Example

**Example 1:**

```
Input: "()"
Output: True
```

**Example 2:**

```
Input: "(*)"
Output: True
```

**Example 3:**

```
Input: "(*))"
Output: True
```

### Note

1. 首先进行最基础的考虑，（在不考虑星号的情况下）我们必定会选择位置最接近的左右括号配对，这样避免了人为造成的右括号前面没有左括号匹配的惨剧。因此我们在写程序进行处理的时候，对于每个右括号判断前面是否有1个左括号能被他拥有，如果左括号数量不足，这个字符串必定是false，或者当整个串被匹配完之后发现有多余的左括号，这个字符串同样是false
2. 接下来考虑有星号的情况:”\)”必须由位置在它之前的”\(”或”_”匹配，如果”\(”或者”_”数量不足导致的false是无法避免的，而如果”\(“ 比”）”多，将”\(”与”_”优先匹配可以减小false的可能性。举个例子如样例3，从左往右遍历的时候，优先匹配”（”和”_”，遇见第一个”\)”，发现没有单独的”\(”,从”\(_”的组合中拆出一个”\(“与之匹配，而原先匹配中的_因为可以等同于不存在便不予理会，接着遇到第二个”\)”,拿走刚才剩余的”_”。综上我们可以观察到，”\(”容易受制于”\)”而将其与”_”匹配后就很灵活，不仅避免了数量太多带来的麻烦，也能在和\*匹配后再次提供自身给”\)”进行匹配。而如果这样匹配结束还有多余的”\(”则必定false
3. 我们设**l（left）为必须被右括号匹配的左括号数量**，**cp（couple）为前面左括号和星号数量**。遍历字符串，遇到左括号和星号的时候,cp++; 遇到右括号的时候cp--; 遇到星号，默认先于前面的左括号\(l&gt;0\)匹配,此时\(l--\)，遇到右括号，默认先与前面必须与右括号匹配的左括号匹配，此时\(l--;c--;\)或者考虑\(cp--\) 注意cp是前方左右的左括号和星号数量，**一旦cp&lt;0即false**. 匹配完发现\(l&gt;0\)即多出了左括号，也为false。剩下的情况就是true了

### Code

```java
class Solution {
    public boolean checkValidString(String s) {
        int l = 0, cp = 0;
        for (char c : s.toCharArray()) {
            if (c == '(') {
                l++;
                cp++;
            } else if (c == '*') {
                if (l > 0) {
                    l--;
                }
                cp++;
            } else {
                if (l > 0) {
                    l--;
                }
                cp--;
                if (cp < 0) {
                    return false;
                }
            }
        }
        
        if (l != 0) {
            return false;
        }
        return true;
    }
}
```



