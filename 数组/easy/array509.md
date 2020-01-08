# leetcode 数组类 斐波那契数

## 解法一

递归解法,当N小于等于1时返回N,否则返回fib(N - 1) + fib(N - 2)

```c++
class Solution {
public:
    int fib(int N) {
      if(N <= 1)
      {
        return N;
      }
      return fib(N - 2) + fib(N - 1);
    }
};
```

## 解法二

非递归解法,将递归改为迭代降低时间复杂度

```c++
class Solution {
public:
    int fib(int N) {
      if(N <= 1)
      {
        return N;
      }
      int first = 0,second = 1,result = 0;
      while((N--) > 1){
        result = first + second;
        first = second;
        second = result;
      }
      return result;
    }
};
```
