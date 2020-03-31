# leetcode 有序数组中出现次数超过25%的元素

## 解法一

此解法比较简单粗暴,用unordered_map记录每个元素出现的次数,当出现符合条件的元素时就返回

```c++
class Solution {
public:
    int findSpecialInteger(vector<int>& arr) {
      int size = arr.size();
      int flag = 0.25 * size;
      int ans = 0;
      int number = 0;
      unordered_map<int,int>record;
      for(int i = 0; i < size; i++) {
        record[arr[i]]++;
        ans = arr[i];
        number = record[arr[i]];
        if(number > flag){
          return ans;
        }
      }
      return ans;
    }
};
```

## 解法二

不使用额外的存储空间,利用数组有序,直接计算每个元素出现的次数

```c++
class Solution {
public:
    int findSpecialInteger(vector<int>& arr) {
      int size = arr.size();
      int flag = 0.25 * size;
      int ans = 0;
      for(int i = 0; i < size; i++) {
        ans = arr[i];
        if(i + flag + 1 < size){
          if(arr[i] == arr[i + flag + 1]){
            return ans;
          }
        }
      }
      return ans;
    }
};
```
