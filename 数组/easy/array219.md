# leetcode 数组类 存在重复元素二

## 解法一

此题要特别注意读懂题意,题目的意思是存在|i - j|<=k即可

```c++
class Solution {
public:
    bool containsNearbyDuplicate(vector<int>& nums, int k) {
      unordered_map<int,int> m;
      int result = 0;
      for(int i = 0; i < nums.size(); i++)
      {
        if(m.find(nums[i]) != m.end())
        {
          result = abs(m[nums[i]] - i);
          if(result <= k)
          {
            return true;
          }
        }
        m[nums[i]] = i;
      }
      return false;
    }
};
```
