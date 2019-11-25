# leetcode 数组类 两数之和

```c++
class Solution  
{  
public:  
 vector<int> twoSum(vector<int>& nums, int target)  
 {  
  unordered_map<int, int> m;  
  for(int i = 0; i < nums.size(); i++)  
    {  
   if(m.count(target - nums[i]))  
   {  
    return {m[target - nums[i]], i};  
   }  
   else  
   {  
    m[nums.at(i)] = i;  
   }  
  }  
  return {0, 0};  
 }  
};
```

解题心得：简单解法利用双重循环遍历加以判断就能找出两数和为目标值的下标，但此解法的时间复杂度为O(n^2),因此需要优化
利用STL中的(unordered_map)以key-value的形式存储索引和索引所对应的值，通过一次循环遍历key值以找出两个数的下标, 时间复杂度为O(1),但空间复杂度会有所上升，以空间换时间是可以接受的
