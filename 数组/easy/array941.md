# leetcode 数组类 有效的山峰数组

## 解法一

正向扫描数组记录第一次山峰出现的下标为left,反向扫描数组记录第一次山峰出现的下标为right,判断left与right是否相等,根据题目设定的边界范围left == 0 或者 right == A.size() - 1时返回false

```c++
class Solution {
public:
    bool validMountainArray(vector<int>& A) {
        if(A.size() < 3)
        {
          return false;
        }
        int left = -1;
        int right = A.size();
        for(int i = 0; i < A.size() - 1; i++)
        {
          if(A[i] >= A[i + 1])
          {
            left = i;
            break;
          }
        }
        for(int j = A.size() - 1; j >= 1; j--)
        {
          if(A[j] >= A[j - 1])
          {
            right = j;
            break;
          }
        }
        if(left == 0 || right == A.size() - 1)
        {
          return false;
        }
        return left == right;
    }
};
```

## 解法二

将解法一的两次遍历改成双指针的一次遍历

```c++
class Solution {
public:
    bool validMountainArray(vector<int>& A) {
        if(A.size() < 3)
        {
          return false;
        }
        int left = -1;
        int right = A.size();
        int i = 0,j = A.size() - 1;
        while(i < A.size() - 1 || j >= 1)
        {
          if(i < A.size() - 1)
          {
            if(A[i] >= A[i + 1])
            {
              left = i;
              i = A.size();
            }else
            {
              i++;
            }
          }
          if(j >= 1)
          {
            if(A[j] >= A[j - 1])
            {
              right = j;
              j = 0;
            }else
            {
              j--;
            }
          }
        }
        if(left == 0 || right == A.size() - 1)
        {
          return false;
        }
        return left == right;
    }
};
```
