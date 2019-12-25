# leetcode 数组类 较大分组位置

## 解法一

遍历字符串,用 temp 保存当前检查元素,count 用于计数,start 记录 temp 元素的下标,当发现与 temp 不同元素时,检查 count 是否大等于 3,若是则将{start,i - 1}加入结果数组 result,当元素与 temp 相同时 count++,由于符合条件元素可能在最后,需要在遍历完字符串后再次检查 count 是否大等于 3,若是则将{start,S.length() - 1}加入结果数组 result,最后返回 result

```c++
class Solution {
public:
    vector<vector<int>> largeGroupPositions(string S) {
      if(S.length() < 3)
      {
        return {};
      }
      vector<vector<int>> result;
      int count = 1;
      char temp = S[0];
      int start = 0;
      for(int i = start + 1; i < S.length(); i++)
      {
        if(S[i] != temp)
        {
          if(count >= 3)
          {
            result.push_back({start,i - 1});
          }
          temp = S[i];
          count = 1;
          start = i;
        }else
        {
          count++;
        }
      }
      if(count >= 3)
      {
        result.push_back({start, S.length() - 1});
      }
      return result;
    }
};
```

经过优化后的双指针解法

```c++
class Solution {
public:
    vector<vector<int>> largeGroupPositions(string S) {
      if(S.length() < 3)
      {
        return {};
      }
      vector<vector<int>> result;
      int i = 0;
      int len = S.length();
      for(int j = 0; j < len; ++j)
      {
        if(j == len - 1 || S[i] != S[j + 1])
        {
          if(j - i + 1 >= 3)
          {
            result.push_back({i,j});
          }
          i = j + 1;
        }
      }
      return result;
    }
};
```
