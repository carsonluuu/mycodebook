# [Restore IP Addresses](https://leetcode.com/problems/restore-ip-addresses/)

Given a string containing only digits, restore it by returning all possible valid IP address combinations.

### **Example**

```
Input:
 "25525511135"

Output:
["255.255.11.135", "255.255.111.35"]
```

### Note

依旧是 DFS + Backtracking，Split String的变体，加了限制条件

每一步有三种可能：选一位数，两位数，还有三位数。切4次 -- ipIndex

一个需要注意的边界条件是当选取多位数时，第一位不能是0，因为 '020' 或 '05' 都不是有效的 IP 地址。

### Code

```java
public class Solution {
    public List<String> restoreIpAddresses(String s) {
        List<String> list = new ArrayList<String>();
        if (s.length() > 12) return list;

        dfs(list, new StringBuilder(), s, 0, 0);

        return list;
    }

    private void dfs(List<String> list, StringBuilder sb, 
                     String s, int ipIndex, int strIndex) {
        if (ipIndex > 4) return;
        if (ipIndex == 4 && strIndex == s.length()) {
            sb.setLength(sb.length() - 1);
            list.add(sb.toString());
            return; 
        }

        int length = sb.length();
        // Add one digit number 
        for (int i = 0; i < 3; i++) {
            if (strIndex + i < s.length()) {
                String substr = s.substring(strIndex, strIndex + 1 + i);
                if (isValid(substr)) {
                    sb.append(substr);
                    sb.append('.');

                    dfs(list, sb, s, ipIndex + 1, strIndex + 1 + i);

                    sb.setLength(length); //backtracking
                }
            }
        }
    }

    private boolean isValid(String str) {
        if (str.charAt(0) == '0') {
            return str.equals("0");
        }
        int num = Integer.parseInt(str);

        if (num > 0 && num <= 255) return true;
        return false;
    }
}
```



