# leetcode 数组类 最长连续递增序列

## 解法一

比较相邻数组元素大小,若右边比左边大则count++,否则重置count,result始终取max(result,count)保证是最长序列,对于数组长度小等于1的直接返回数组长度

```c++
class Solution {
public:
    int findLengthOfLCIS(vector<int>& nums) {
      if(nums.size() <= 1)
      {
        return nums.size();
      }
      int count = 1;
      int result = INT_MIN;
        for(int i = 0; i < nums.size() - 1; i++)
        {
          if(nums[i + 1] > nums[i])
          {
            count++;
          }else
          {
            count = 1;
          }
          result = max(result,count);
        }
        return result;
    }
};
```
