# leetcode 数组类 数组中的k-diff数对

## 解法一

利用两个set容器分别存放符合条件的结果和供查询的集合,最后返回结果集合的大小

```c++
class Solution {
public:
  int findPairs(vector<int>& nums, int k) {
    if(k < 0)
    {
      return 0;
    }
    set<int>s1;
    set<int>s2;
    for(auto x:nums)
    {
      if(s1.find(x + k) != s1.end())
      {
        s2.insert(x);
      }
      if(s1.find(x - k) != s1.end())
      {
        s2.insert(x - k);
      }
      s1.insert(x);
    }
    return s2.size();
  }
};
```
