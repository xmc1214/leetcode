# leetcode 数组类 旋转数组

## 解法一

利用额外的数组空间存放旋转过程中的元素,最后交换两个数组元素

```c++
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
     vector<int> v(nums.size());
     for(int i = 0; i < nums.size(); i++)
     {
       v[(i + k) % nums.size()] = nums[i];
     }
     swap(v,nums);
    }
};
```

## 解法二

利用反转函数进行三次反转得到结果,此处对k进行一个简化处理

```c++
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
      k %= nums.size();
      reverse(nums.begin(),nums.end());
      reverse(nums.begin(),nums.begin() + k);
      reverse(nums.begin() + k,nums.end());
    }
};
```

以下是手写reverse函数的实现版本

```c++
class Solution {
public:
  void reverse(int start,int end,vector<int> &nums)
  {
    while(start < end)
    {
      int temp = nums[start];
      nums[start] = nums[end];
      nums[end] = temp;
      start++;
      end--;
    }
  }
  void rotate(vector<int>& nums, int k) {
    k %= nums.size();
    reverse(0,nums.size() - 1,nums);
    reverse(0,k - 1,nums);
    reverse(k,nums.size() - 1,nums);
  }
};

```
