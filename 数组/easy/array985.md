# leetcode 数组类 查询后的偶数和

## 解法一

此解法无法通过全部测试用例,模拟整个过程,时间复杂度太高

```c++
class Solution {
public:
    vector<int> sumEvenAfterQueries(vector<int>& A, vector<vector<int>>& queries) {
      int val = 0, index = 0;
      vector<int>result(A.size());
      for(int i = 0; i < A.size(); i++)
      {
        val = queries[i][0];
        index = queries[i][1];
        A[index] += val;
        result[i] = sumOfOdd(A);
      }
      return result;
    }
    int static sumOfOdd(vector<int>& A) {
      int ans = 0;
      for(auto x:A) {
        if(x % 2 == 0) {
          ans += x;
        }
      }
      return ans;
    }
};
```

## 解法二

解法一超时的原因是双重循环,解法二将遍历A.size()次A求解偶数和优化为初始求解,每次局部求解偶数的变化

```c++
class Solution {
public:
    vector<int> sumEvenAfterQueries(vector<int>& A, vector<vector<int>>& queries) {
      int val = 0, index = 0;
      vector<int>result(A.size());
      int ans = 0;
      for(auto x:A) {
        if(x % 2 == 0) {
          ans += x;
        }
      }
      for(int i = 0; i < A.size(); i++)
      {
        val = queries[i][0];
        index = queries[i][1];
        result[i] = ans;
        if((A[index] + val) % 2 == 0)
        {
          if(A[index] % 2 == 0)
          {
            result[i] += val;
          }else
          {
            result[i] += A[index] + val;
          }
        }else
        {
          if(A[index] % 2 == 0)
          {
            result[i] -= A[index];
          }
        }
        ans = result[i];
        A[index] += val;
      }
      return result;
    }
};
```
