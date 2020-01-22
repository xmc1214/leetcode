# leetcode 数组类 将数组分成和相等的三个部分

## 解法一

先求解出数组和的三分之一,遍历数组每组合出一个和就计数加一,遍历结束后再次检查，若次数为三则返回为true,否则返回false

```c++
class Solution {
public:
    bool canThreePartsEqualSum(vector<int>& A) {
      int result = accumulate(A.begin(),A.end(),0) / 3;
      int count = 0;
      int temp = 0;
      for(int i = 0; i < A.size(); i++) {
        if(temp == result) {
          count++;
          temp = 0;
        }
        temp += A[i];
      }
      if(temp == result) {
        count++;
      }
      return count == 3;
    }
};
```
