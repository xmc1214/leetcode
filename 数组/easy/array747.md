# leetcode 数组类 至少是其他数字的两倍大

## 解法一

利用额外的数组空间进行升序后找到最大元素,遍历原数组,如果元素与最大元素相等则保存下标,否则判断该元素的两倍是否大于最大元素,若是则返回-1,若不是则继续遍历

```c++
class Solution {
public:
    int dominantIndex(vector<int>& nums) {
      if(nums.size() < 1)
      {
        return -1;
      }
      int max = INT_MIN;
      int size = nums.size();
      vector<int>temp = nums;
      sort(temp.begin(),temp.end());
      for(int i = 0; i < size; i++)
      {
        if(nums[i] == temp[size - 1])
        {
          max = i;
        }else if(nums[i] * 2 > temp[size - 1])
        {
          return -1;
        }
      }
      return max;
    }
};
```

## 解法二

利用c++内置算法求得最大值以及下标,再进行数组遍历检查该最大值是否符合条件

```c++
class Solution {
public:
    int dominantIndex(vector<int>& nums) {
      int maxValue = *max_element(nums.begin(),nums.end()); 
      int maxPosition = max_element(nums.begin(),nums.end()) - nums.begin();
      for(int i = 0; i < nums.size(); i++)
      {
        if(nums[i] != maxValue)
        {
          if(nums[i] * 2 > maxValue)
          {
            return -1;
          }
        }
      }
      return maxPosition;
    }
};
```
