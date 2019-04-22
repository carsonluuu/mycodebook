# Replace all occurrences of string AB with C

Given a string **str **that may contain one more occurrences of “AB”. Replace all occurrences of “AB” with “C” in str.

### ** Examples**

```
Input  : str = "helloABworld"
Output : str = "helloCworld"

Input  : str = "fghABsdfABysu"
Output : str = "fghCsdfCysu"
```

### Note

In-place做法：需要双指针记录pattern，符合移动快指针，不符合copy over，快慢指针同时跳过

### Code

```java
static void translate(char str[]) { 
    int len = str.length; 
    if (len < 2) return; 

    // Index in modified string 
    int i = 0; 

    // Index in original string 
    int j = 0;  

    // Traverse string 
    while (j < len - 1) 
    { 
        // Replace occurrence of "AB" with "C" 
        if (str[j] == 'A' && str[j + 1] == 'B') 
        { 
            // Increment j by 2 
            j = j + 2; 
            str[i++] = 'C'; 
            continue; 
        } 
        str[i++] = str[j++]; 
    } 

    if (j == len - 1) 
    str[i++] = str[j]; 

    // add a null character to terminate string 
    str[i] = ' '; 
    str[len - 1]=' '; 
}
```

"ab" to "c" and "b" to "ef"

"b" to "ef" 需要反向，且需要知道额外长度

```py
class Repalce():
    def ab_to_c(self, s):
        length = len(s)

        if length < 2:
            return

        i = 0  # Index in modified string
        j = 0  # Index in original string

        count = 0  # number of b after replacement

        # Traverse string
        while j < length - 1:
            if s[j] == 'a' and s[j + 1] == 'b':
                j += 2  # Increment j by 2
                s[i] = 'c'
                i += 1
                continue

            if s[i] == 'b':
                count += 1

            s[i] = s[j]
            i += 1
            j += 1

        if j == length - 1:
            s[i] = s[j]
            i += 1

        # add a null character to terminate string
        s[i] = ' '
        s[length - 1] = ' '

        print(count)
        print(i)
        print(j)
        return i, count

    def b_to_ef(self, s, length, plus_length):
        i = length + plus_length - 1
        j = length - 1

        while j >= 0:
            if s[j] == 'b':
                s[i] = 'f'
                s[i - 1] = 'e'
                i -= 2
                j -= 1
                continue

            s[i] = s[j]
            i -= 1
            j -= 1
        print(i)
        print(j)

    def replace_patterns(self, s):
        length, plus_length = self.ab_to_c(self, s)
        self.b_to_ef(self, length, plus_length, s)


if __name__ == '__main__':
    s = list("wabcbabbabxyab")
    r = Repalce()
    length, plus_length = r.ab_to_c(s)
    print(s)
    r.b_to_ef(s, length, plus_length)
    print(s)

```



