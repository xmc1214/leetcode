# leetcode 数组类 买卖股票最佳时机

## 解法一

简单动态规划,遍历找出最佳的买入时间,期间result保存最大利润

```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
      if(prices.size() <= 1)
      {
        return 0;
      }
      int result = 0;
      int buy = prices[0];
      for(int i = 1; i < prices.size(); i++)
      {
        if(prices[i] > buy)
        {
          result = max(result,prices[i] - buy);
        }else
        {
          buy = prices[i];
        }
      }
      return result;
    }
};

```
