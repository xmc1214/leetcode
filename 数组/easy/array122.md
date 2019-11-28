# leetcode 数组类 买卖股票最佳时机二

## 解法一

相对于第一题而言逻辑部分改动,result保存的不是一次交易可以达到的最大利润,而是每次能产生利润的交易的利润和

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
          result = result + prices[i] - buy;
        }
        buy = price[i];
      }
      return result;
    }
};

```
