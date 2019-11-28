# leetcode 数组类 搜索插入位置

## 解法一

直接遍历数组,如果数组元素大于或者等于target就返回下标,否则遍历结束后返回数组大小为下标

```c++
class Solution
{
public:
 int searchInsert(vector<int>& nums, int target)
 {
  for(int i = 0; i < nums.size(); i++)
  {
   if(nums[i] >= target)
   {
    return i;
   }
  }
  return nums.size();
 }
};
```

## 解法二

利用STL中的二分查找函数lower_bound()返回第一个大于或者等于target的迭代器,再与起始迭代器相减得到下标,target小于等于nums第一个元素的情况额外处理

```c++
class Solution {
public:
  int searchInsert(vector<int>& nums, int target) {
    if(target <= nums[0])
    {
      return 0;
    }
    return lower_bound(nums.begin(),nums.end(),target) - nums.begin();
  }
};
```

## 解法三

手写二分查找,如果mid等于target则返回mid,循环结束后返回left

```c++
class Solution {
public:
  int searchInsert(vector<int>& nums, int target) {
    if(nums.size() == 0)
    {
      return 0;
    }
    int left = 0;
    int right = nums.size() - 1;
    while(left <= right)
    {
      int mid = left + (right - left) / 2;
      if(nums[mid] == target)
      {
        return mid;
      }else if(nums[mid] < target)
      {
        left = mid + 1;
      }else{
        right = mid - 1;
      }
    }
    return left;
  }
};
```
