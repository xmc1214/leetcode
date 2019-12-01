# leetcode 数组类 移动零

## 解法一

利用快慢指针,遍历数组将非零元素移至慢指针所指下标,再将慢指针后到数组结尾的元素全部置为0

```c++
class Solution {
public:
  void moveZeroes(vector<int>& nums) {
    int j = 0;
    for(int i = 0; i < nums.size(); i++)
    {
      if(nums[i] != 0)
      {
        nums[j++] = nums[i];
      }
    }
    while(j < nums.size())
    {
      nums[j++] = 0;
    }
  }
};
```

## 解法二

针对解法一的部分优化,当快指针所指元素非0时,将快指针所指元素与慢指针所指元素交换,慢指针加一,快指针加一,否则只有快指针加一

```c++
class Solution {
public:
  void moveZeroes(vector<int>& nums) {
    int i = 0;
    int j = 0;
    while(i < nums.size())
    {
      if(nums[i] != 0)
      {
        swap(nums[j++],nums[i]);
      }
      i++;
    }
  }
};
```
