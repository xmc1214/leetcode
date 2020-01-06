# leetcode 数组类 按奇偶排序数组 II

## 解法一

两次遍历数组,第一次遍历将数组中的偶数放入新数组的偶数下标对应位置,第二次遍历将数组中奇数放入新数组的奇数下标对应位置

```c++
class Solution
{
public:
 vector<int> sortArrayByParityII(vector<int>& A)
 {
  vector<int>result(A.size());
  int j = 0;
  for(int i = 0; i < A.size(); i++)
  {
    if(A[i] % 2 == 0)
    {
      result[j] = A[i];
      j += 2;
    }
  }
  int t = 1;
  for(int i = 0; i < A.size(); i++)
  {
    if(A[i] % 2 != 0)
    {
      result[t] = A[i];
      t += 2;
    }
  }
  return result;
  }
};
```

## 解法二

利用双指针,只要将偶数都置于偶数下标位置,则奇数也会位于奇数位置,在奇数位置每找到一个偶数就与偶数位置的奇数交换

```c++
class Solution
{
public:
  vector<int> sortArrayByParityII(vector<int>& A)
  {
    int j = 1;
    for (int i = 0; i < A.size(); i += 2)
      if (A[i] % 2 == 1)
      {
        while (A[j] % 2 == 1)
          j += 2;

        // Swap A[i] and A[j]
        int tmp = A[i];
        A[i] = A[j];
        A[j] = tmp;
      }
    return A;
  }
};
```
