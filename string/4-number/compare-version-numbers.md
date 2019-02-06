# [Compare Version Numbers](https://leetcode.com/problems/compare-version-numbers/description/)

Compare two version numbers_version1_and_version2_.  
If_`version1`_`>`_`version2`_return`1;` if_`version1`_`<`_`version2`_return`-1;`otherwise return`0`.

You may assume that the version strings are non-empty and contain only digits and the`.`character.

The`.`character does not represent a decimal point and is used to separate number sequences.

For instance,`2.5`is not "two and a half" or "half way to version three", it is the fifth second-level revision of the second first-level revision.

You may assume the default revision number for each level of a version number to be`0`. For example, version number`3.4`has a revision number of`3`and`4`for its first and second level revision number. Its third and fourth level revision number are both`0`.

### Example

**Example 1:**

```
Input:
version1
 = "0.1", 
version2
 = "1.1"

Output:
 -1
```

**Example 2:**

```
Input: 
version1
 = "1.0.1", 
version2
 = "1"

Output:
 1
```

**Example 3:**

```
Input:
version1
 = "7.5.2.4", 
version2
 = "7.5.3"

Output:
 -1
```

**Example 4:**

```
Input:
version1
 = "1.01", 
version2
 = "1.001"

Output:
 0

Explanation:
 Ignoring leading zeroes, both “01” and “001" represent the same number “1”
```

**Example 5:**

```
Input:
version1
 = "1.0", 
version2
 = "1.0.0"

Output:
 0

Explanation:
 The first version number does not have a third level revision number, 
 which means its third level revision number is default to "0"
```

### Note



### Code

```java
class Solution {
    public int compareVersion(String version1, String version2) {
        String[] v1 = version1.split("\\.");
        String[] v2 = version2.split("\\.");
        for (int i = 0; i < Math.max(v1.length, v2.length); i++) {
            int num1 = i < v1.length? Integer.parseInt(v1[i]) : 0;
            int num2 = i < v2.length? Integer.parseInt(v2[i]) : 0;
            if (num1 < num2) {
                return -1;
            }
            else if (num1 > num2) {
                return 1;
            }
        }
        return 0;        
    }

}
```



