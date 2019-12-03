# leetcode 数组类 找到所有数组中消失的数字

## 解法一

常规解法使用额外的set容器存放数组元素,遍历1～n在set容器中查找是否存在,若不存在则加入返回的数组中

```c++
class Solution {
public:
    vector<int> findDisappearedNumbers(vector<int>& nums) {
      set<int> s;
      vector<int> v;
      for(auto x:nums)
      {
        s.insert(x);
      }
      for(int i = 1; i <= nums.size(); i++)
      {
        if(s.find(i) == s.end())
        {
          v.push_back(i);
        }
      }
      return v;
    }
};
```

## 解法二

使用额外的数组空间初始化元素值为0,遍历原数组将元素减一作为额外数组的下标,对其所对应的值加一,遍历额外数组若元素为0则返回数组加入该下标加一的值

```c++
class Solution {
public:
    vector<int> findDisappearedNumbers(vector<int>& nums) {
        vector<int> hasht(nums.size(), 0);
        for(auto n : nums)
            hasht[n - 1]++;
        vector<int> res;
        for(int i = 0; i < nums.size(); i++){
            if(hasht[i] == 0) res.push_back(i + 1);
        }
        return res;
    }
};
```

## 解法三

与解法二相似,区别是没有使用额外的空间,直接在原数组上进行元素交换

```c++
class Solution {
public:
    vector<int> findDisappearedNumbers(vector<int>& nums) {
      vector<int> v;
      for(int i = 0; i < nums.size(); i++)
      {
        while(nums[nums[i] - 1] != nums[i])
        {
          swap(nums[nums[i] - 1],nums[i]);
        }
      }
      for(int j = 0; j < nums.size(); j++)
      {
        if(nums[j] != j + 1)
        {
          v.push_back(j + 1);
        }
      }
      return v;
    }
};
```
