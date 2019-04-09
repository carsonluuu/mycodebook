# [Edit Distance](https://leetcode.com/problems/edit-distance/description/)

Given two words _word1 _and _word2_, find the minimum number of operations required to convert _word1 _to _word2_.

You have the following 3 operations permitted on a word:

1. Insert a character
2. Delete a character
3. Replace a character

### **Example**

**Example 1:**

```
Input:
 word1 = "horse", word2 = "ros"

Output:
 3

Explanation:
 
horse -> rorse (replace 'h' with 'r')
rorse -> rose (remove 'r')
rose -> ros (remove 'e')
```

**Example 2:**

```
Input:
 word1 = "intention", word2 = "execution"

Output:
 5

Explanation:
 
intention -> inention (remove 't')
inention -> enention (replace 'i' with 'e')
enention -> exention (replace 'n' with 'x')
exention -> exection (replace 'n' with 'c')
exection -> execution (insert 'u')
```

### Note

Let's go further and introduce an edit distance`D[i][j]`which is an edit distance between the first`i`characters of`word1`and the first`j`characters of`word2`.

![](https://leetcode.com/problems/edit-distance/Figures/72/72_edit.png "edit\_distance")It turns out that one could compute`D[i][j]`, knowing`D[i - 1][j]`,`D[i][j - 1]`and`D[i - 1][j - 1]`.

There is just one more character to add into one or both strings and the formula is quite obvious.

If the last character is the same,_i.e._`word1[i] = word2[j]`then

`D[i][j]=1+min(D[i−1][j],D[i][j−1],D[i−1][j−1]−1)`

and if not, _i.e. _`word1[i] != word2[j]`we have to take into account the replacement of the last character during the conversion.



`D[i][j]=1+min(D[i−1][j],D[i][j−1],D[i−1][j−1])`



So each step of the computation would be done based on the previous computation, as follows:

![](https://leetcode.com/problems/edit-distance/Figures/72/72_compute.png "compute")

The obvious base case is an edit distance between the empty string and non-empty string that means`D[i][0] = i`and`D[0][j] = j`.



