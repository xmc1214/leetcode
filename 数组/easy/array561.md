# leetcode 数组类 数组拆分I

## 解法一

根据题意可得若要数对中得最小值之和最大则需要数对之间的差值尽可能的小,故排序后的数组相邻元素组成的数对就满足要求

```c++
class Solution {
public:
    int arrayPairSum(vector<int>& nums) {
      sort(nums.begin(),nums.end());
      int sum = 0;
      for(int i = 0; i < nums.size(); i += 2)
      {
        sum += nums[i];
      }
      return sum;
    }
};
```
