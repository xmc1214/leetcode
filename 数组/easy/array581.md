# leetcode 数组类 最短无序连续数组

## 解法一

比较简单的解法就是将原数组的副本排序后与原数组进行首尾对比分别找出第一个不相等的元素的下标,下标差加一就是结果,此外需要对原数组就是有序数组的特殊情况进行特判,之所以能这么做是因为题目限定了连续

```c++
class Solution {
public:
    int findUnsortedSubarray(vector<int>& nums) {
       vector<int>v(nums.begin(),nums.end());
       sort(v.begin(),v.end());
       if(v == nums)
       {
         return 0;
       }
       int low = 0;
       int high = 0;
       for(int i = 0,j = nums.size() - 1; i < nums.size(),j > 0; i++,j--)
       {
         if(nums[i] != v[i])
         {
           low = i;
           break;
         }
       }
       for(int j = nums.size() - 1; j > 0; j--)
       {
         if(nums[j] != v[j])
         {
           high = j;
           break;
         }
       }
       return high - low + 1;
    }
};
```
