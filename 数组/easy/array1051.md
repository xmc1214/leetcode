# leetcode 高度检查器

## 解法一

拷贝一份原数组进行升序排序，与原数组进行对比，碰到不相同的元素则count++

```c++
class Solution {
public:
    int heightChecker(vector<int>& heights) {
      vector<int>result = heights;
      sort(result.begin(),result.end());
      int count = 0;
      if(heights.size() == 0) {
        return count;
      }
      for(int i = 0; i < heights.size(); i++) {
        if(heights[i] != result[i]) {
          count++;
        }
      }
      return count;
    }
};
```
