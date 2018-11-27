# [Split String](https://www.lintcode.com/problem/split-string/description?_from=ladder&&fromId=1)

Give a string, you can choose to split the string after one character or two adjacent characters, and make the string to be composed of only one character or two characters. Output all possible results.

### Example

Given the string`"123"`  
return`[["1","2","3"],["12","3"],["1","23"]]`

### Note

枚举分1或者分2的情况

传参数的时候是有两种写法的，一种是传下标（dfsHelper），一种是传子串（dfs）可能后者比较直观一些，本质都是一样滴

Time complexity: O\(\(2^n\)\)

Space complexity: O\(\(2^n\)\)

### Code

```java
public class Solution {
    /*
     * @param : a string to be split
     * @return: all possible split string array
     */
    public List<List<String>> splitString(String s) {
        // write your code here
        List<List<String>> results = new ArrayList<>();
        if (s == null) {
            return results;
        } else if (s.length() == 0) {
            results.add(new ArrayList<>());
            return results;
        }

        //dfsHelper(results, new ArrayList<>(), 0, s);
        dfs(results, new ArrayList<>(), s);

        return results;
    }

    private void dfs(List<List<String>> results, 
                     List<String> list,
                     String s) {
        if (s.equals("")) {
            results.add(new ArrayList<>(list));
            return;
        }          

        for (int i = 1; i <= 2; i++) {
            if (i <= s.length()) {
                list.add(s.substring(0, i));
                dfs(results, list, s.substring(i));
                list.remove(list.size() - 1);
            }
        }
    }

    private void dfsHelper(List<List<String>> results,
                           List<String> result,
                           int index,
                           String s) {
        if (index == s.length()) {
            results.add(new ArrayList<>(result));
            return;
        }

        for (int i = index; i < index + 2 && i < s.length(); i++) {
            String substring = s.substring(index, i + 1);
            result.add(substring);
            dfsHelper(results, result, i + 1, s);
            result.remove(result.size() - 1);
        }
    }
}
```



