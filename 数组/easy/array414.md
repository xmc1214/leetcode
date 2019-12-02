# leetcode 数组类 第三大的数

## 解法一

利用内置排序将数组升序,再利用去重容器将重复移至数组尾部将至删除,判断数组长度是否小于3,若小于则直接返回最后一个元素,否则返回倒数第三个元素

```c++
class Solution {
public:
  int thirdMax(vector<int>& nums) {
    sort(nums.begin(),nums.end());
    vector<int>::iterator it = unique(nums.begin(),nums.end());
    nums.erase(it,nums.end());
    if(nums.size() < 3)
    {
      return nums[nums.size() - 1];
    }
    return nums[nums.size() - 3];
  }
};
```
