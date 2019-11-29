# leetcode 数组类 存在重复元素

## 解法一

利用sort对数组进行排序使相同元素位于相邻位置,使用adjacent_find查找相邻重复元素,若存在则返回true,否则返回false

```c++
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
      sort(nums.begin(),nums.end());
      vector<int>::iterator it = adjacent_find(nums.begin(),nums.end());
      if(it != nums.end())
      {
        return true;
      }
      return false;
    }
};
```
