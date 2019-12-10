# leetcode 数组类 子数组最大平均数 I

## 解法一

利用滑动窗口只保存 k 个数字和,通过取减去第一个数字加上第 k+1 个数字和的最大值求得最大平均数

```c++
class Solution {
public:
    double findMaxAverage(vector<int>& nums, int k) {
      double n = 0;
      double mx = 0;
      int i = 0;
      for(i = 0; i < k; i++)
      {
        n += nums[i];
      }
      mx = n;
      for(i = k; i < nums.size(); i++)
      {
        n += nums[i];
        n -= nums[i - k];
        mx = max(n, mx);
      }
      return mx / k;
    }
};
```
