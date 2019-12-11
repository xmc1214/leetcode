# leetcode 数组类 图片平滑器

## 解法一

遍历数组每个元素对其边界进行判定,决定元素和以及元素个数,逐一对元素和求平均值再存入新的数组

```c++
class Solution {
public:
    vector<vector<int>> imageSmoother(vector<vector<int>>& M) {
      int row = M.size();
      int col = M[0].size();
      vector<vector<int>>res(row, vector<int>(col, 0));
      for(int i = 0; i < row; ++i){
          for(int j = 0; j < col; ++j){
              int count = 0;
              for(int t = i - 1; t <= i + 1; t++)
              {
                for(int m = j - 1; m <= j + 1; m++)
                {
                  if(t < row && t >= 0 && m < col && m >= 0)
                  {
                    res[i][j] += M[t][m];
                    count++;
                  }
                }
              }
              res[i][j] /= count;
          }
      }
      return res;
  }
};
```
