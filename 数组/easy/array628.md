# leetcode 数组类 三个数最大的乘积

## 解法一

将数组排序后三个数的最大乘积在最后三个数乘积和前两个数与最后一个数乘积之间取最大值

```c++
class Solution {
public:
  int maximumProduct(vector<int>& nums) {
    sort(nums.begin(),nums.end());
    int size = nums.size();
    return max(nums[0] * nums[1] * nums[size - 1],nums[size - 1] * nums[size - 2] * nums[size - 3]);
  }
};
```

## 解法二

如果不使用排序可以通过遍历数组找出最大的三个数和最小的两个数

```c++
class Solution {
public:
  int maximumProduct(vector<int>& nums) {
    int min1 = INT_MAX;
    int min2 = INT_MAX;
    int max1 = INT_MIN;
    int max2 = INT_MIN;
    int max3 = INT_MIN;
    for(auto x:nums)
    {
      if(x <= min1)
      {
        min2 = min1;
        min1 = x;
      }else if(x <= min2)
      {
        min2 = x;
      }
      if(x >= max1)
      {
        max3 = max2;
        max2 = max1;
        max1 = x;
      }else if(x >= max2)
      {
        max3 = max2;
        max2 = x;
      }else if(x >=max3)
      {
        max3 = x;
      }
    }
    return max(min1 * min2 * max1,max1 * max2 * max3);
  }
};
```
