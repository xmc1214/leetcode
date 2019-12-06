# leetcode 数组类 种花问题

## 解法一

通过首尾补0可以避免对于边界的判断,连续出现三个0就能在中间种一朵花,对n进行判断可以优化执行次数

```c++
class Solution {
public:
    bool canPlaceFlowers(vector<int>& flowerbed, int n) {
      flowerbed.insert(flowerbed.begin(),0);
      flowerbed.push_back(0);
      for(int i = 1; i < flowerbed.size() - 1; i++)
      {
        if(flowerbed[i - 1] == 0 && flowerbed[i] == 0 && flowerbed[i + 1] == 0)
        {
          flowerbed[i] =1;
          n--;
        }
        if(n == 0)
        {
          return true;
        }
      }
      return n <= 0;
    }
};
```
