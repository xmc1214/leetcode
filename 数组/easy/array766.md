# leetcode 数组类 托普利茨矩阵

## 解法一

遍历二维矩阵的行,每次将行矩阵存入数组,遍历数组计算元素对角线上的相邻元素是否相等,若不等则返回false,否则遍历完矩阵的行后返回true

```c++
class Solution {
public:
    bool isToeplitzMatrix(vector<vector<int>>& matrix) {
      vector<int>v;
      for(int i = 0; i < matrix.size() - 1; i++)
      {
        v = matrix[i];
        for(int j = 0; j < v.size() - 1; j++)
        {
          int x = i + 1;
          int y = j + 1;
          if(v[j] != matrix[x][y])
          {
            return false;
          }
        }
      }
      return true;
    }
};
```
