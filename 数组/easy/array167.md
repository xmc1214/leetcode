# leetcode 数组类 两数之和二-输入有序数组

## 解法一

思路与两数之和基本一致,可参照第一题

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& numbers, int target) {
        unordered_map<int, int> um;
        for(int i = 0; i < numbers.size(); i++)
        {
          if(um.count(target - numbers[i]))
          {
            return {um[target - numbers[i]] + 1,i + 1};
          }else
          {
            um[numbers[i]] = i;
          }
        }
        return {0,0};
    }
};

```
