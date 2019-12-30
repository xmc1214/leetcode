# leetcode 数组类 转置矩阵

## 解法一

初始化一个以原数组列和行作为行和列的新数组,利用双重循环重新将列数组放入新数组的行

```c++
class Solution {
public:
    vector<vector<int>> transpose(vector<vector<int>>& A) {
        vector<vector<int>> result(A[0].size(),vector<int>(A.size()));
        for(int i = 0; i < A[0].size(); i++)
        {
          for(int j = 0; j < A.size(); j++)
          {
            result[i][j] = A[j][i];
          }
        }
        return result;
    }
};
```
