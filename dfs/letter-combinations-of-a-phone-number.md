# Letter Combinations of a Phone Number

Given a string containing digits from`2-9`inclusive, return all possible letter combinations that the number could represent.

A mapping of digit to letters \(just like on the telephone buttons\) is given below. Note that 1 does not map to any letters.

![](http://upload.wikimedia.org/wikipedia/commons/thumb/7/73/Telephone-keypad2.svg/200px-Telephone-keypad2.svg.png)

### Example

```
Input: "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
```

### Note1

类似笛卡尔积，需要建立数字和字母的映射

`private final String[] mappings = {"", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"}`

index控制第几个数字，终止条件即index遍历完号码，同时dfs遍历每个映射内部的字母

### Code1

```java
class Solution {

    private final String[] mappings = {"", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};

    public List<String> letterCombinations(String digits) {
        List<String> res = new ArrayList<>();
        if (digits == null || digits.length() == 0) return res;
        helper(res, digits, "", 0);
        return res;
    }

    public void helper(List<String> res, String digits, String s, int index){
        if (index == digits.length()) {
            res.add(s); 
            return;
        }

        String letters = mappings[digits.charAt(index) - '0'];

        for (int i = 0; i < letters.length(); i++) {
            helper(res, digits, s + letters.charAt(i), index + 1);
        }
    }
}
```

### Note2

BFS方法，队列里增加的是长度逐渐增加的结果，其长度就是BFS的层数

第一层 a b c

第二层 对之前每个元素加上 d e f

当字符串长度和数字长度一致时，就加入结果

### Code2

```java
class Solution {

    private final String[] mappings = {"", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};

    public List<String> letterCombinations(String digits) {
        List<String> res = new ArrayList<>();
        if (digits == null || digits.length() == 0) return res;
        Queue<String> queue = new LinkedList<>();
        queue.offer("");
        while (!queue.isEmpty()) {
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                String word = queue.poll();
                if (word.length() < digits.length()) {
                    int digit = digits.charAt(word.length()) - '0';
                    for (char c : mappings[digit].toCharArray()) {
                        queue.offer(word + c);
                    }
                } else {
                    res.add(word);
                }
            }
        }
        return res;
    }
}
```



