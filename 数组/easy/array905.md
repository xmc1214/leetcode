# leetcode 数组类 按奇偶排序数组

## 解法一

利用内置sort排序算法自定义排序规则将偶数放在奇数前面

```c++
class Solution {

bool static oddEven(int a,int b) {
  return (a % 2) < (b % 2);
}
public:
    vector<int> sortArrayByParity(vector<int>& A) {
      sort(A.begin(),A.end(),oddEven);
      return A;
    }
};
```

## 解法二

利用两次遍历分别将偶数和奇数筛选到新的数组内

```c++
class Solution {
public:
    vector<int> sortArrayByParity(vector<int>& A) {
      vector<int>result(A.size());
      int t = 0;
      for(int i = 0; i < A.size(); i++)
      {
        if(A[i] % 2 == 0)
        {
          result[t++] = A[i];
        }
      }
       for(int j = 0; j < A.size(); j++)
      {
        if(A[j] % 2 != 0)
        {
          result[t++] = A[j];
        }
      }
      return result;
    }
};
```

## 解法三

利用双端队列结构,在头部插入偶数,在尾部插入奇数,最后将双端队列转换成数组

```c++
class Solution {
public:
    vector<int> sortArrayByParity(vector<int>& A) {
      deque<int>result;
      for(auto x:A){
        if(x % 2 == 0)
        {
          result.push_front(x);
        }else{
          result.push_back(x);
        }
      }
      vector<int>v(make_move_iterator(result.begin()),make_move_iterator(result.end()));
      return v;
    }
};
```

## 解法四

利用双指针low,high遍历数组,保证low之前的下标元素都是偶数,high之后的下标元素都是奇数,直到low>=high结束遍历

```c++
class Solution {
public:
    vector<int> sortArrayByParity(vector<int>& A) {
      int low = 0;
      int high = A.size() - 1;
      while(low < high)
      {
        if(A[low] % 2 > A[high] % 2)
        {
          A[low] = A[low] + A[high];
          A[high] = A[low] - A[high];
          A[low] = A[low] - A[high];
        }
        if(A[low] % 2 == 0)low++;
        if(A[high] % 2 != 0) high--;
      }
      return A;
    }
};
```
