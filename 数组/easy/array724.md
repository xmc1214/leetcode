# leetcode 数组类 寻找数组中心索引

## 解法一

遍历数组求和保存在sum中,再次遍历数组当left_count = sum - nums[i] - left_count时说明下标i左右元素和相等

```c++
class Solution {
public:
    int pivotIndex(vector<int>& nums) {
      if(nums.size() == 0)
      {
        return -1;
      }
      int sum = 0;
      for(auto x:nums)
      {
        sum += x;
      }
      int left_count = 0;
      for(int i = 0; i < nums.size(); i++)
      {
        if(left_count == sum - nums[i] - left_count)
        {
          return i;
        }
        left_count += nums[i];
      }
      return -1;
    }
};
```