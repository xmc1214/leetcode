# leetcode 数组类 非递减数列

## 解法一

通过比较相邻的元素大小,如果左元素大于右元素则尝试减小左元素或者增大右元素后再次比较左右元素大小,每次改变计数加一,最后计数大于一就返回 false

```c++
class Solution {
public:
    bool checkPossibility(vector<int>& nums) {
      int cnt = 0;
      for(int i = 0; i < nums.size() - 1; i++)
      {
        if(nums[i] > nums[i + 1]) {
            int tmp = nums[i];
            if(i >= 1) {
                nums[i] = nums[i - 1];
            } else {
                nums[i] = nums[i + 1];
            }
            if(nums[i] > nums[i + 1]) {
                nums[i] = tmp;
                nums[i + 1] = nums[i];
            }
            cnt++;
            if(cnt == 2) {
                return false;
            }
        }
      }
      return true;
    }
};
```
