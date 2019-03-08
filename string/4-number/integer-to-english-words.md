# [Integer to English Words](https://leetcode.com/problems/integer-to-english-words/description/)

Convert a non-negative integer to its english words representation. Given input is guaranteed to be less than 2^31- 1.

### Example

**Example 1:**

```
Input:
 123

Output:
 "One Hundred Twenty Three"
```

**Example 2:**

```
Input:
 12345

Output:
 "Twelve Thousand Three Hundred Forty Five"
```

**Example 3:**

```
Input:
 1234567

Output:
 "One Million Two Hundred Thirty Four Thousand Five Hundred Sixty Seven"
```

**Example 4:**

```
Input:
 1234567891

Output:
 "One Billion Two Hundred Thirty Four Million Five Hundred Sixty Seven Thousand Eight Hundred Ninety One"
```

### Note

O\(1\)时间

### Code

```java
class Solution {
    private final String[] LESS_THAN_20 = {"", "One", "Two", "Three", "Four", "Five",
                                           "Six", "Seven", "Eight", "Nine", "Ten", 
                                           "Eleven", "Twelve", "Thirteen", "Fourteen", "Fifteen",
                                           "Sixteen", "Seventeen", "Eighteen", "Nineteen"}; //20
    private final String[] TENS = {"", "Ten", "Twenty", "Thirty", "Forty", "Fifty", 
                                   "Sixty", "Seventy", "Eighty", "Ninety"}; //10
    private final String[] THOUSANDS = {"", "Thousand", "Million", "Billion"}; //4

    public String numberToWords(int num) {
        if (num == 0) return "Zero";

        int i = 0;
        String words = "";

        while (num > 0) {
            if (num % 1000 != 0) {
                words = helper(num % 1000) + THOUSANDS[i] + " " + words;
            }
            num /= 1000;
            i++;
        }

        return words.trim();
    }

    private String helper(int num) {
        if (num == 0) {
            return "";
        } 
        if (num < 20) {
            return LESS_THAN_20[num] + " ";
        }
        if (num < 100) {
            return TENS[num / 10] + " " + helper(num % 10);
        }
        
        return LESS_THAN_20[num / 100] + " Hundred " + helper(num % 100);
    }
}
```



