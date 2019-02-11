# [Nested List Weight Sum](https://leetcode.com/problems/nested-list-weight-sum/description/)

Given a nested list of integers, return the sum of all integers in the list weighted by their depth.

Each element is either an integer, or a list -- whose elements may also be integers or other lists.

### Example

**Example 1:**

```
Input: [[1,1],2,[1,1]]
Output: 10 
Explanation: Four 1's at depth 2, one 2 at depth 1.
```

**Example 2:**

```
Input: [1,[4,[6]]]
Output: 27 
Explanation: One 1 at depth 1, one 4 at depth 2, and one 6 at depth 3; 1 + 4*2 + 6*3 = 27.
```

### Note

DFS 传递list和层数

### Code

```py
class Solution:
    def depthSum(self, nestedList: 'List[NestedInteger]') -> 'int':
        def dfs(nestedList, level):
            if not nestedList:
                return 0
            sum = 0
            for elem in nestedList:
                if elem.isInteger():
                    sum += elem.getInteger() * level
                else:
                    sum += dfs(elem.getList(), level + 1)
            return sum
        return dfs(nestedList, 1)
```

如果深度反过来，要么存成list然后处理一下结果

要么累加，之前多被加几层

```py
class Solution:
    def depthSumInverse(self, nestedList: 'List[NestedInteger]') -> 'int':
        total, level = 0, 0
        while len(nestedList):
            nextLevel = []
            for x in nestedList:
                if x.isInteger():
                    level += x.getInteger()
                else:
                    for y in x.getList():
                        nextLevel.append(y)
            total += level
            nestedList = nextLevel
        return total
```



