# leetcode 拼写单词

## 解法一

利用unorder_map存储记录chars中每个字母出现的次数，遍历words对每个字符串进行对比，每出现一个字母就将chars中相应的key的value减一，当value小等于0时终止对比，不符合条件，利用flag进行标识，每次内层循环结束时flag为true则ans = ans + words[i].size(),每次外层循环都需要将temp,flag重置。

```c++
class Solution {
public:
    int countCharacters(vector<string>& words, string chars) {
    unordered_map<char, int> basic;
    unordered_map<char, int> temp;
    int ans = 0;
    int flag = true;
    for(char ele : chars)
    {
      if(basic.find(ele) != basic.end())
      {
        basic[ele]++;
      }
      else
      {
        basic.insert(make_pair(ele, 1));
      }
    }
    for(int i = 0; i < words.size(); i++)
    {
      flag = true;
      temp = basic;
      for(int j = 0; j < words[i].size(); j++)
      {
        if(temp[words[i].at(j)] <= 0)
        {
          flag = false;
          break;
        }
        else
        {
          temp[words[i].at(j)]--;
        }
      }
      if(flag)
      {
        ans += words[i].size();
      }
    }
    return ans;
  }
};
```
