# [Dungeon Game](https://leetcode.com/problems/dungeon-game/description/)

The demons had captured the princess \(**P**\) and imprisoned her in the bottom-right corner of a dungeon. The dungeon consists of M x N rooms laid out in a 2D grid. Our valiant knight \(**K**\) was initially positioned in the top-left room and must fight his way through the dungeon to rescue the princess.

The knight has an initial health point represented by a positive integer. If at any point his health point drops to 0 or below, he dies immediately.

Some of the rooms are guarded by demons, so the knight loses health \(_negative_integers\) upon entering these rooms; other rooms are either empty \(_0's_\) or contain magic orbs that increase the knight's health \(_positive_integers\).

In order to reach the princess as quickly as possible, the knight decides to move only rightward or downward in each step.



**Write a function to determine the knight's minimum initial health so that he is able to rescue the princess.**

### Example

For example, given the dungeon below, the initial health of the knight must be at least **7 **if he follows the optimal path`RIGHT-> RIGHT -> DOWN -> DOWN`.

| -2 \(K\) | -3 | 3 |
| :--- | :--- | :--- |
| -5 | -10 | 1 |
| 10 | 30 | -5 \(P\) |

**Note:**

* The knight's health has no upper bound.
* Any room can contain threats or power-ups, even the first room the knight enters and the bottom-right room where the princess is imprisoned.

### Note

利用DP矩阵，反向倒推生命值。

```
down  = Math.max(health[i + 1][j] - dungeon[i][j], 1)
right = Math.max(health[i][j + 1] - dungeon[i][j], 1);
```

最差也必须是1，针对的是正数的情况，相减会更小，取最大为1（所有格子都是正数，那么1血升天）

所以初始化也是`health[m - 1][n - 1] = Math.max(1 - dungeon[m - 1][n - 1], 1)`

初始化还需要把最下行和最右列初始化了

最后维护每一步的最小值为DP矩阵的值 `health[i][j] = Math.min(right, down)`

### Code

```java
class Solution {
    public int calculateMinimumHP(int[][] dungeon) {
        if (dungeon == null || dungeon.length == 0 || dungeon[0].length == 0) return 0;

        int m = dungeon.length;
        int n = dungeon[0].length;

        int[][] health = new int[m][n];

        health[m - 1][n - 1] = Math.max(1 - dungeon[m - 1][n - 1], 1);

        for (int i = m - 2; i >= 0; i--) {            
            health[i][n - 1] = Math.max(health[i + 1][n - 1] - dungeon[i][n - 1], 1);
        }

        for (int j = n - 2; j >= 0; j--) {
            health[m - 1][j] = Math.max(health[m - 1][j + 1] - dungeon[m - 1][j], 1);
        }
        
        for (int i = m - 2; i >= 0; i--) {
            for (int j = n - 2; j >= 0; j--) {
                int down = Math.max(health[i + 1][j] - dungeon[i][j], 1);
                int right = Math.max(health[i][j + 1] - dungeon[i][j], 1);
                health[i][j] = Math.min(right, down);
            }
        }
        
        return health[0][0];
    }
}
```



