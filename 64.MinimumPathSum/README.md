### 题意
题目：最小路径和  
给定一个m x n的格子，格子中每个位置填充满非负数，找到一条从左上右下的路径，保证该路径上所有数字的和是所有满足要求的路径中最小的.  
注意: 在任何一个点只能向下或者向右移动.  

### 题解
**算法及复杂度（9 ms）**  
本题和第62、63题类似.  
本题是一道进行搜索的题目，显然可以通过暴力搜索完成.但是暴力搜索的复杂度会达到幂数量级，应该尝试找到一种更好的方法.  
看到本题，从62题和63题的做题经验来看，看到这种全局限制性的路径问题（本题的限制条件是只能向右或者向下前进），可以考虑使用动态规划的问题进行求解.  
仔细分析本题，到达点（m, n）的路径一定经过（m - 1, n）或者（m, n - 1）.也就是说，到达（m, n）的最小路径（即所有路径中路径上所有数值和最小的路径）一定是到达（m - 1, n）的最小路径或者到达（m, n - 1）的最小路径.因此，题目可以转化为求到达（m - 1, n）的最小路径和到达（m, n - 1）的最小路径.一次递推下去.就形成了最优子结构性质.  
依据上边的分析，可以看到，从起点到达每个点的最小路径值就可以当做一个状态，如果设dp[i][j]是从起始点（1, 1）到点（i, j）的最小路径值，那么状态转移方程也就是`dp[i][j] = min(dp[i - 1][j], dp[i][j - 1]) + grid[i][j], 其中i,j >= 1, i <= m, j <= n`.显然这个状态是无后效性的（即本状态不受本点之后的状态的影响）.通过简单的二重循环就可以对以上方程求解.  
**时间复杂度:** O(mn). 二重循环，对表格中每一个位置求解.  
**代码参见本文件夹下solution.cpp**  

### 算法正确性
**正确性证明**  
最优子结构性质和无后效性性质保证能够使用动态规划求解.通过以下例子可以进一步理解状态转移的过程.  
**举个例子**  
```  
//输入数据 grid = [[1, 2, 3], [1, 2, 1]]

//初始化
dp[0][0] = grid[0][0] = 1

//显然第0行和第0列的状态只能通过前一状态得到
dp[0][1] = dp[0][0] + grid[0][1] = 3
dp[0][2] = dp[0][1] + grid[0][2] = 6
dp[1][0] = dp[0][0] + grid[1][0] = 2

//接下来进行for训练，外层是行，内层是列，直接训练第1行，从第1列开始
dp[1][1] = min(dp[0][1] + dp[1][0]) + grid[1][1] = 4
dp[1][2] = min(dp[0][2] + dp[1][1]) + grid[1][2] = 5

//返回结果
return dp[1[2] = 5
```  