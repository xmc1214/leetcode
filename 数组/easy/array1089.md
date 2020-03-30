# leetcode 复写零

## 解法一

将需要复写的零按照下标插入，同时将数组末尾的元素弹出，若数组最后一个元素为零则不做操作

```c++
class Solution {
public:
    void duplicateZeros(vector<int>& arr) {
      int i = 0;
      while(i < arr.size()) {
        if(arr[i] == 0) {
          if(i != arr.size() - 1){
            arr.insert(arr.begin() + i,0);
            arr.pop_back();
            i += 2;
          }else{
            i++;
          }
        }else{
          i++;
        }
      }
    }
};
```
