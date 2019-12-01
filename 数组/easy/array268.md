# leetcode 数组类 缺失的数字

## 解法一

使用排序的方式,将原数组进行升序,然后通过对相邻元素差值是否大于一判断缺失的数值,需要对首尾数字进行特判

```c++
class Solution {
public:
    int missingNumber(vector<int>& nums) {
      sort(nums.begin(),nums.end());
      if(nums[nums.size() - 1] != nums.size())
      {
        return nums.size();
      }
      if(nums[0] != 0)
      {
        return 0;
      }
      for(int i = 0; i < nums.size() - 1; i++)
      {
        if(nums[i + 1] - nums[i] != 1)
        {
          return (i + 1);
        }
      }
      return -1;
    }
};
```

## 解法二

同样利用数组升序,然后将0～n的数字放入额外的数组空间,遍历原数组元素与新数组元素做比较,若不相等则返回新数组元素,遍历结束后直接返回剩下的新数组的元素

```c++
class Solution {
public:
    int missingNumber(vector<int>& nums) {
      sort(nums.begin(),nums.end());
      vector<int> v;
      for(int i = 0; i <= nums.size(); i++)
      {
        v.push_back(i);
      }
      int j = 0;
      while(j < nums.size())
      {
        if(nums[j] != v[j])
        {
          return v[j];
        }
        j++;
      }
      return v[j];
    }
};
```

## 解法三

利用set自动升序存放数组元素,然后逐一查找0～n的元素是否存在于set中,若不存在则返回该元素

```c++
class Solution {
public:
    int missingNumber(vector<int>& nums) {
      set<int> s;
      for(auto x:nums)
      {
        s.insert(x);
      }
      for(int i = 0; i <= nums.size(); i++)
      {
        if(s.find(i) == s.end())
        {
          return i;
        }
      }
      return -1;
    }
};
```

## 解法四

利用异或运算,两个相同的数字进行异或会得到0,最后剩下的元素就是缺失的数字

```c++
class Solution {
public:
    int missingNumber(vector<int>& nums) {
      int res = nums.size();
        for (int i = 0; i < nums.size(); i++){
            res = i ^ nums[i] ^ res;
        }
        return res;
    }
};
```

## 解法五

利用等差数列求和公式求出0～n的数字和,再遍历数组逐一减去数组元素,最后的结果就是缺失的数字

```c++
class Solution {
public:
    int missingNumber(vector<int>& nums) {
      int res = nums.size();
      int sum = res*(res + 1) / 2;
      for(auto x:nums)
      {
        sum -= x;
      }
      return sum;
    }
};
```
