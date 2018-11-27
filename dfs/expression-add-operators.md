# Expression Add Operators

Given a string that contains only digits`0-9`and a target value, return all possibilities to add **binary **operators \(not unary\)`+`,`-`, or`*`between the digits so they evaluate to the target value.

### Example

**Example 1:**

```
Input:
num = "123", 
target = 6

Output: 
["1+2+3", "1*2*3"]
```

**Example 2:**

```
Input:
num = "232", 
target = 8

Output: 
["2*3+2", "2+3*2"]
```

**Example 3:**

```
Input:
num = "105", 
target = 5

Output: 
["1*0+5","10-5"]
```

**Example 4:**

```
Input:
num = "00", 
target = 0

Output: 
["0+0", "0-0", "0*0"]
```

**Example 5:**

```
Input:
num = "3456237490", 
target = 9191

Output: 
[]
```

### Note

1. overflow: we use a long type once it is larger than Integer.MAX\_VALUE or minimum, we get over it.

2. 0 sequence: because we can't have numbers with multiple digits started with zero, we have to deal with it too

3. a little trick is that we should save the value that is to be multiplied in the next recursion.

存之前的值，对于1 + 23，在2和3之间加入”\*“，1+2+2\*3-2，需要减掉之前保存的值来维持运算的优先级。

对于0，剪枝的原则：起始零，如01，00，02等情况，需要容忍单个0的情况。`i != start && num.charAt(start) == '0'`

初始化时start为0，加入当前的值，不做运算操作

```
流程：
1. dfs + backtracking 思路
2. dfs 函数中存 "左面表达式的当前值" 和 "上一步操作的结果" (用于处理优先级)
3. 参数都用 Long，防止溢出，毕竟 String 可能是个大数
4. 如果 start 位置是 0 而且当前循环的 index 还是 0，直接 return，因为一轮循环只能取一次 0；
5. start == 0 的时候，直接考虑所有可能的起始数字扔进去，同时更新 cumuVal 和 prevVal;
6. 除此之外，依次遍历所有可能的 curVal parse，按三种不同的可能操作做 dfs + backtracking;
   - 加法：直接算，prevVal 参数传 curVal，代表上一步是加法；
   - 减法：直接算，prevVal 参数传 -curVal，代表上一步是减法；
   - 乘法：要先减去 prevVal 抹去上一步的计算，然后加上 prevVal curVal 代表当前值；同时传的 preVal 参数也等于 prevVal curVal. 
   - 乘法操作这种处理方式，在遇到连续乘法的时候可以看到是叠加的；但是前一步操作如果不是乘法，则可以优先计算乘法操作。

10-5-2x6 ，遇到乘法之前是 cumuVal = 3, preVal = -2; 
新一轮 dfs 时 curVal = 6, 先退回前一步操作 - prevVal，得到 5，
其实就是之前 (10 - 5) 的结果，然后加上当前结果 (-2 x 5)，prevVal 设成 -10 传递过去即可。
```

### Code

```java
class Solution {
    public List<String> addOperators(String num, int target) {
        List<String> res = new ArrayList<>();

        dfs(num, target, res, "", 0, 0, 0);

        return res;
    }

    private void dfs(String num, int target, List<String> res, 
                     String s, long sum, long lastValue, int start) {
        if (start == num.length()) {
            if (sum == target) {
                res.add(s);
            }
            return;
        }

        for (int i = start; i < num.length(); i++) {
            if (i != start && num.charAt(start) == '0') {
                break;
            } 
            long curr = Long.parseLong(num.substring(start, i + 1));
            if (start == 0) {
                dfs(num, target, res, "" + curr, curr, curr, i + 1);
            } else {
                dfs(num, target, res, s + "*" + curr, 
                    sum + curr * lastValue - lastValue, curr * lastValue, i + 1);
                dfs(num, target, res, s + "+" + curr, sum + curr,  curr,  i + 1);
                dfs(num, target, res, s + "-" + curr, sum - curr, -curr,  i + 1);
            }
        }
    }
}
```



