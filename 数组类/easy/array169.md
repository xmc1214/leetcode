# leetcode 数组类 多数元素

## 解法一

投票算法,众数一定比其他数的个数之和要大,遍历数组令每个元素为target,初始个数为1,相同元素个数加一,不同元素个数减一,若count为0,则更换target,遍历结束后target就是众数

```c++
class Solution
{
public:
 int majorityElement(vector<int>& nums)
 {
    int target = nums[0];
    int count = 1;
    for(int i = 1; i < nums.size(); i++)
    {
      if(nums[i] != target)
      {
        count--;
        if(count == 0)
        {
          target = nums[i];
          count = 1;
        }
      }
      else
      {
        count++;
        if(count > nums.size() / 2)
        {
          return target;
        }
      }
    }  
    return target;
  }
};
```

## 解法二

利用哈希表遍历数组存储每个元素和对应的元素个数,当找到个数大于数组长度一半的value时返回key值

```c++
class Solution
{
public:
 int majorityElement(vector<int>& nums)
 {
  int size = nums.size() / 2;
  unordered_map<int,int> m;
    for(auto x:nums)
    {
      m[x]++;
      if(m[x] > size)
      {
        return x;
      }
    }
    return 0;
 }
};
```
