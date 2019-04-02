# Reverse

**Example 1:**

```
Input:
 "Let's take LeetCode contest"

Output:
 "s'teL ekat edoCteeL tsetnoc"
```

```java
class Solution {
    public String reverseWords(String s) {
        String[] str = s.split(" ");
        for (int i = 0; i < str.length; i++) {
            str[i] = new StringBuilder(str[i]).reverse().toString();
        }
        
        StringBuilder result = new StringBuilder();
        for (String st : str) {
            result.append(st + " ");
        }
        
        return result.toString().trim();        
    }
}
```

**Example 2:**

```
Input: "the sky is blue"

Output: 
"blue is sky the"
```

```
public class Solution {
    public String reverseWords(String s) {
        if (s == null || s.length() == 0) return s;
        StringBuilder sb = new StringBuilder ();
        String[] words = s.trim().split("\\s+");
        
        for (int i = words.length - 1; i >= 0; i--) {
            sb.append(words[i] + " ");
        }
        
        return sb.toString().trim();
    }
}
```

**Example 3:**

```
Input:  
["t","h","e"," ","s","k","y"," ","i","s"," ","b","l","u","e"]

Output: 
["b","l","u","e"," ","i","s"," ","s","k","y"," ","t","h","e"]
```

```java
// 三步翻转法
class Solution {
    public void reverseWords(char[] str) {
        swap(str, 0, str.length - 1);
        int start = 0;
        for (int i = 0; i < str.length; i++) {
            if (str[i] == ' ') {
                swap(str, start, i - 1);
                start = i + 1;
            }
        }
        
        swap(str, start, str.length - 1);
        
    }
    
    private void swap(char[] str, int i, int j) {
        while (i < j) {
            char temp = str[i];
            str[i++] = str[j];
            str[j--] = temp;    
        }
    }
}
```



