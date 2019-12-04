# leetcode 数组类 最大连续1的个数

## 解法一

使用一个变量m保存最大连续一的个数,count保存每次连续一的个数,当碰到不为1的数字时，m的值是max(m,count),最后再判断一遍防止整个数组都是一的情况

```c++
class Solution {
public:
  int findMaxConsecutiveOnes(vector<int>& nums) {
    int count = 0;
    int m = 0;
    for(int i = 0; i < nums.size(); i++)
    {
      if(nums[i] == 1)
      {
        count++;
      }else
      {
        m = max(m,count);
        count = 0;
      }
      m = max(m,count);
    }
    return m;
  }
};
```
