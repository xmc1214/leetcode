# leetcode 数组类 有序数组的平方

## 解法一

直接先将数组元素改为原来的平方,再使用自带排序算法sort升序

```c++
class Solution {
public:
    vector<int> sortedSquares(vector<int>& A) {
      for(int i = 0; i < A.size(); i++)
      {
        A[i] = A[i] * A[i];
      }
      sort(A.begin(),A.end());
      return A;
    }
};
```

## 解法二

利用双指针正向遍历正数元素,反向遍历负数元素,再将元素归并到一个新的数组

```c++
class Solution {
public:
    bool static compare(int val)
    {
      return val < 0;
    }
    vector<int> sortedSquares(vector<int>& A) {
      vector<int> result(A.size());
      int j = count_if(A.begin(),A.end(),compare);
      int i = j - 1;
      int t = 0;
      while(i >= 0 && j < A.size())
      {
        if(A[i] * A[i] < A[j] * A[j])
        {
          result[t++] = A[i] * A[i];
          i--;
        }else
        {
          result[t++] = A[j] * A[j];
          j++;
        }
      }
      while(i >= 0)
      {
        result[t++] = A[i] * A[i];
        i--;
      }
      while(j < A.size())
      {
        result[t++] = A[j] * A[j];
        j++;
      }
      return result;
    }
};
```
