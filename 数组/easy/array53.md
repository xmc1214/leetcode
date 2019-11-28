# leetcode 数组类 最大子序列和

## 解法一

双重循环每次外循环都将sum置为0,内循环寻找比max大的值

```c++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int max = INT_MIN;
        int numSize = nums.size();
        for(int i = 0; i < numSize; i++)
        {
          int sum = 0;
          for(int j = i; j < numSize; j++)
          {
            sum += nums[j];
            if(sum > max)
            {
              max = sum;
            }
          }
        }
        return max;
    }
};
```

## 解法二

利用动态规划,dp保存局部最优解,即取前一次的最优解dp加上nums[i]与nums[i]中的最大值,result保存整体最优解,即取result和dp之间的最大值

```c++
class Solution
{
public:
    int maxSubArray(vector<int> &nums)
    {
        //类似寻找最大最小值的题目，初始值一定要定义成理论上的最小最大值
        int result = INT_MIN;
        int numsSize = int(nums.size());
        int dp(nums[0]);
        result = dp;
        for (int i = 1; i < numsSize; i++)
        {
            dp = max(dp + nums[i], nums[i]);
            result = max(result, dp);
        }
        return result;
    }
};

```
