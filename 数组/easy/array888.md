# leetcode 数组类 公平的糖果交换

## 解法一

暴力法,双重循环遍历两个数组的元素,判断交换元素后的两数组和是否相等,若相等则返回两个元素,若不相等则继续遍历

```c++
class Solution {
public:
    vector<int> fairCandySwap(vector<int>& A, vector<int>& B) {
        int sumA = accumulate(A.begin(),A.end(),0);
        int sumB = accumulate(B.begin(),B.end(),0);
        for(int i = 0; i < A.size(); i++)
        {
          for(int j = 0; j < B.size(); j++)
          {
            if(sumA - A[i] + B[j] == sumB + A[i] - B[j])
            {
              return {A[i],B[j]};
            }
          }
        }
        return {};
    }
};
```

## 解法二

分别计算两个数组的初始和,将两个数组进行升序排序,定义两个指针i,j分别指向两个数组,用newA和newB保存交换后的数组和,判断是否相等,若相等则返回i,j所指元素,若newA大于newB说明A[i]需要增大,i++,反之B[j]需要增大,j++

```c++
class Solution {
public:
    vector<int> fairCandySwap(vector<int>& A, vector<int>& B) {
        int sumA = accumulate(A.begin(),A.end(),0);
        int sumB = accumulate(B.begin(),B.end(),0);
        sort(A.begin(),A.end());
        sort(B.begin(),B.end());
        int i = 0,j = 0;
        while(i < A.size() || j < B.size())
        {
          int newA = sumA + B[j] - A[i];
          int newB = sumB - B[j] + A[i];
          if(newA == newB)
          {
            return {A[i],B[j]};
          }else if(newA > newB)
          {
            if(i < A.size())
            {
              i++;
            }
          }else if(newA < newB)
          {
            if(j < B.size())
            {
              j++;
            }
          }
        }
        return {};
    }
};
```