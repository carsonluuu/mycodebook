# [Text Justification](https://leetcode.com/problems/text-justification/description/)

Given an array of words and a width _maxWidth_, format the text such that each line has exactly_maxWidth_characters and is fully \(left and right\) justified.

You should pack your words in a greedy approach; that is, pack as many words as you can in each line. Pad extra spaces`' '`when necessary so that each line has exactly_maxWidth_characters.

Extra spaces between words should be distributed as evenly as possible. If the number of spaces on a line do not divide evenly between words, the empty slots on the left will be assigned more spaces than the slots on the right.

For the last line of text, it should be left justified and no**extra**space is inserted between words.

**Note:**

* A word is defined as a character sequence consisting of non-space characters only.
* Each word's length is guaranteed to be greater than 0 and not exceed _maxWidth_.
* The input array `words`contains at least one word.

### Example

**Example 1:**

```
Input:

words = ["This", "is", "an", "example", "of", "text", "justification."]
maxWidth = 16

Output:

[
   "This    is    an",
   "example  of text",
   "justification.  "
]

```

**Example 2:**

```
Input:

words = ["What","must","be","acknowledgment","shall","be"]
maxWidth = 16

Output:

[
  "What   must   be",
  "acknowledgment  ",
  "shall be        "
]

Explanation:
 Note that the last line is "shall be    " instead of "shall     be",
             because the last line must be left-justified instead of fully-justified.
             Note that the second line is also left-justified becase it contains only one word.

```

**Example 3:**

```
Input:

words = ["Science","is","what","we","understand","well","enough","to","explain",
         "to","a","computer.","Art","is","everything","else","we","do"]
maxWidth = 20

Output:

[
  "Science  is  what we",
  "understand      well",
  "enough to explain to",
  "a  computer.  Art is",
  "everything  else  we",
  "do                  "
]
```

### Note

实现题

利用取余来进行计算空格

### Code

```java
/*
  16
  -----
  4 (3) 4 (3) 2 | (16 - 4 - 4 - 2)/3 = 2
  7 (2) 2 (1) 4 | (16 - 7 - 2 - 4)/3 = 1 (16 - 7 - 2 - 4)%3 = 1  
  5 (1) 2 (8)   |
  "What   must   be"
  "example  of text"
  "shall be        "
*/
class Solution {
    public List<String> fullJustify(String[] words, int L) {
        List<String> res = new ArrayList<>();
        int i = 0; //word index
        int len = words.length;
        while (i < len) {
            int count = words[i].length();
            int j = i + 1; //one row's last word index
            while (j < len) {
                if (count + words[j].length() + 1 > L) break;
                count += words[j].length() + 1;
                j++;//will jump to the new begginning line head
            }
            StringBuilder sb = new StringBuilder();
            sb.append(words[i]);
            int diff = j - i - 1; //4 - 0 - 1 = 3 or 1 - 0 - 1 = 0 
            //last line case
            if (diff == 0 || j == len) {
                for (int k = i + 1; k < j; k++) {
                    sb.append(" " + words[k]);
                }
                for (int k = sb.length(); k < L; k++) {
                    sb.append(" ");
                }
            } else {
                int space = (L - count) / diff;
                int r = (L - count) % diff;
                for (int k = i + 1; k < j; k++) {
                    for (int l = space; l > 0; l--) {
                        sb.append(" ");
                    }
                    if (r > 0) {
                        sb.append(" ");
                        r--;
                    }
                    sb.append(" " + words[k]);
                }
            }
            res.add(sb.toString());
            i = j;
        }        
        return res;
    }
}
```



