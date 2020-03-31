# leetcode 数组的相对排序

## 解法一

使用map记录升序后arr1的各元素个数,遍历arr2先将record中在arr2出现的元素插入arr3,并将其value至为零,遍历record将剩余的元素插入arr3,最后返回arr3

```c++
class Solution {
public:
    vector<int> relativeSortArray(vector<int>& arr1, vector<int>& arr2) {
      sort(arr1.begin(),arr1.end());
      map<int,int>record;
      vector<int>arr3;
      for(int i = 0; i < arr1.size(); i++) {
        record[arr1[i]]++;
      }
      for(int j = 0; j < arr2.size(); j++) {
        int number = record.count(arr2[j]);
        if(number != 0) {
          arr3.insert(arr3.end(),record[arr2[j]],arr2[j]);
          record[arr2[j]] = 0;
        }
      }
      for(auto t = record.begin(); t != record.end(); t++) {
        if(t->second != 0) {
          arr3.insert(arr3.end(),t->second,t->first);
        }
      }
      return arr3;
    }
};

```
