# leetcode 数组类 杨辉三角

## 解法一

开头和结尾均为一，中间的数等于左上方的数与右上方的数相加得出

```c++
class Solution {
public:
    vector<vector<int>> generate(int numRows) {
        vector<vector<int>> v(numsRows);
        if(numRows == 0)
        {
          return v;
        }
        for(int i = 0; i < numRows; i++)
        {
          for(int j = 0; j <= i; j++)
          {
            if(i == j || j == 0)
            {
              v[i].push_back(1);
            }else
            {
              v[i].push_back(v[i - 1][j - 1] + v[i - 1][j]);
            }
          }
        }
        return v;
    }
};

```
