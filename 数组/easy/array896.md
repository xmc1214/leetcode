# leetcode 数组类 单调数列

## 解法一

由于题目并未要求判断是单增还是单减,故可以先通过遍历数组使用start记录第一个两元素差值不为零的值,再次遍历数组判断相邻元素差值与start的乘积是否小于零,若是则不是单调数列,返回false,否则遍历结束后返回true

```c++
class Solution {
public:
    bool isMonotonic(vector<int>& A) {
      int start = 0;
      for(int j = 0; j < A.size() - 1; j++)
      {
        if(A[j + 1] - A[j] != 0)
        {
          start = A[j + 1] - A[j];
          break;
        }
      }
      for(int i = 1; i < A.size() - 1; i++)
      {
        if((A[i + 1] - A[i]) * start < 0)
        {
          return false;
        }
      }
      return true;
    }
};
```

## 解法二

此解法是解法一的优化,将两次遍历优化为一次遍历

```c++
class Solution {
public:
    bool isMonotonic(vector<int>& A) {
        int flag=0,store;
        for(int i=0;i<A.size()-1;i++)
        {
            if(A[i]==A[i+1]) continue;
            if(A[i]!=A[i+1]) store=A[i]-A[i+1];
            if(flag*store<0) return false;
            flag=store;
        }
        return true;
    }
};
```
