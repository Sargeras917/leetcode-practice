### 剑指offer-47.礼物的最大价值


##### 1.题目
在一个 m*n 的棋盘的每一格都放有一个礼物，每个礼物都有一定的价值（价值大于 0）。你可以从棋盘的左上角开始拿格子里的礼物，并每次向右或者向下移动一格、直到到达棋盘的右下角。给定一个棋盘及其上面的礼物的价值，请计算你最多能拿到多少价值的礼物？


##### 2.示例
示例1:
```
输入: 
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
输出: 12
解释: 路径 1→3→5→2→1 可以拿到最多价值的礼物
```

##### 3.思路
- 1.这是一个二次列表，要求最后一项的最大值，要找出最后一项上方或者左方的最大值。
- 2.可以直接推出状态转移方程 `dp[i][j] = max(dp[i - 1][j], dp[i][j - 1]) + grid[i][j]`。
- 3.同时要考虑一些边界情况，在最左方时(`j=0`)，`dp[i][j] = dp[i - 1][j] + grid[i][j]`。
- 4.在最上方时(`i=0`)，`dp[i][j] = dp[i][j - 1] + grid[i][j]`
- 5.如果`i=0, j=0`，那么直接返回`grid[0][0]`

##### 4.代码
```javascript
/**
 * @param {number[][]} grid
 * @return {number}
 */
var maxValue = function(grid) {
  const dp = new Array(grid.length).fill(new Array(grid[0].length).fill(0));
  for(let i = 0; i < grid.length; i++) {
    for(let j = 0; j < grid[0].length; j++) {
      if (i === 0 && j === 0) {
        dp[i][j] = grid[i][j];
      } else if (i === 0) {
        dp[i][j] = dp[i][j - 1] + grid[i][j];
      } else if (j === 0) {
        dp[i][j] = dp[i - 1][j] + grid[i][j];
      } else {
        dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]) + grid[i][j];
      }
    }
  }

  return dp[grid.length - 1][grid[0].length -1]
};
```