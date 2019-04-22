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



