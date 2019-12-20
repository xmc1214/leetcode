# leetcode 数组类 使用最小代价爬楼梯

## 解法一

此题需要先正确理解题意,动态转移方程为dp[i] = min(dp[i - 1],dp[i - 2]) + cost[i],最后取min(dp[size - 1],dp[size - 2])即可

```c++
class Solution {
public:
    int minCostClimbingStairs(vector<int>& cost) {
      int size = cost.size();
      vector<int>dp(3,0);
      dp[0] = cost[0];
      dp[1] = cost[1];
      for(int i = 2; i < size; i++)
      {
        dp[i % 3] = min(dp[(i - 1) % 3], dp[(i - 2) % 3]) + cost[i];
      }
      return min(dp[(size - 1) % 3],dp[(size - 2) % 3]);
    }
};
```
