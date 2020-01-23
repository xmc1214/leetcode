# leetcode 数组类 可被五整除的二进制前缀

## 解法一

利用取模运算规则将每一次从数组中取出的元素加上temp左移一位后的值与5求余,若等于0则加入true,否则加入false

```c++
class Solution {
public:
    vector<bool> prefixesDivBy5(vector<int>& A) {
     int temp = 0;
      vector<bool> result;
      for(int i = 0; i < A.size(); i++) {
        temp = ((temp << 1) + A[i]) % 5;
        if(temp == 0) {
          result.push_back(true);
        }else {
          result.push_back(false);
        }
      }
      return result;
    }
};
```
