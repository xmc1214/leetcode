# leetcode 数组类 数组形式的整数加法

## 解法一

逐位相加,判断进位,若数组长度N小于数字K的位数,则将剩余位数的数字逐一插入原数组头部,判断进位,循环结束后还需判断一次进位

```c++
class Solution {
public:
    vector<int> addToArrayForm(vector<int>& A, int K) {
      if(K == 0){
        return A;
      }
      int temp = 0;
      int flag = 0;
      int N = A.size() - 1;
      while(N >= 0 || K > 0)
      {
        temp = K % 10;
        if(N >= 0)
        {
          A[N] += flag;
          flag = (temp + A[N]) / 10;
          A[N] = (temp + A[N]) % 10;
          N--;
        }else
        {
          A.insert(A.begin(), (temp + flag) % 10);
          flag = (temp + flag) / 10;
        }
        K = K / 10;
      }
      if(A[0] == 0 || flag > 0)
      {
        A.insert(A.begin(),1);
      }
      return A;
    }
};
```

## 解法二

使用双端队列将每次计算的值插入队列头部,最后将队列转换为数组

```c++
class Solution {
public:
    vector<int> addToArrayForm(vector<int>& A, int K) {
        deque<int> result;
        int lastNum=K,i=A.size()-1;
        while(i>=0||lastNum>0)
        {
            //对应位相加
            if(i>=0)lastNum+=A[i--];

            //尾部数字添加到result中，同时k需要丢弃尾部数字
            result.push_front(lastNum%10);
            lastNum/=10;
        }
        vector<int> ans(result.size());
        for(int i = 0; i < result.size(); i++)
        {
          ans[i] = result[i];
        }
        return ans;
    }
};
```
