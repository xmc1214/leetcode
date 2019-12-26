# leetcode 数组类 翻转图像

## 解法一

利用stl中的reverse算法对每个子数组进行水平翻转后,再遍历子数组进行反转图片

```c++
class Solution {
public:
    vector<vector<int>> flipAndInvertImage(vector<vector<int>>& A) {
        for(vector<vector<int>>::iterator it = A.begin(); it != A.end(); it++)
        {
          reverse((*it).begin(),(*it).end());
          for(vector<int>::iterator vit = (*it).begin(); vit != (*it).end(); vit++)
          {
            *vit = *vit ^ 1;
          }
        }
        return A;
    }
};
```
