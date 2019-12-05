# leetcode 数组类 重塑数组

## 解法一

使用额外的空间将原数组元素以一维的形式存入,再按照测试案例中给定的行和列将元素放入新数组

```c++
class Solution {
public:
    vector<vector<int>> matrixReshape(vector<vector<int>>& nums, int r, int c) {
        if(nums[0].size() * nums.size() != r * c || nums.size() == 0)
        {
          return nums;
        }
        vector<vector<int>>result(r,vector<int>(c,0));
        queue<int>q;
        for(auto x:nums)
        {
          for(auto y:x)
          {
            q.push(y);
          }
        }
        for(int i = 0; i < r; i++)
        {
          for(int j = 0; j < c; j++)
          {
            result[i][j] = q.front();
            q.pop();
          }
        }
        return result;
    }
};
```

## 解法二

不使用额外的空间,在遍历原数组的时候根据新数组的行列判断将元素直接存入新数组

```c++
class Solution {
public:
    vector<vector<int>> matrixReshape(vector<vector<int>>& nums, int r, int c) {
        if(nums[0].size() * nums.size() != r * c)
        {
          return nums;
        }
        vector<vector<int>>result(r,vector<int>(c,0));
        int h = 0;
        int l = 0;
        for(int i = 0; i < nums.size(); i++)
        {
          for(int j = 0; j < nums[0].size(); j++)
          {
            result[h][l++] = nums[i][j];
            if(l == c)
            {
              h++;
              l = 0;
            }
          }
        }
        return result;
    }
};
```

## 解法三

相对于解法二的区别是直接计算新数组的下标值,不用每次进行判断

```c++
class Solution {
public:
    vector<vector<int>> matrixReshape(vector<vector<int>>& nums, int r, int c) {
        if(nums[0].size() * nums.size() != r * c)
        {
          return nums;
        }
        vector<vector<int>>result(r,vector<int>(c,0));
        int count = 0;
        for(int i = 0; i < nums.size(); i++)
        {
          for(int j = 0; j < nums[0].size(); j++)
          {
            result[count / c][count % c] = nums[i][j];
            count++;
          }
        }
        return result;
    }
};

```
