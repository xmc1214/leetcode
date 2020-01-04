# leetcode 数组类 卡牌分组

## 解法一

利用最大公约数即可求解

```c++
class Solution {
public:
    bool hasGroupsSizeX(vector<int>& deck) {
    vector<int>count(10000);
        for (auto c: deck)
            count[c]++;

        int g = -1;
        for (int i = 0; i < 10000; ++i)
            if (count[i] > 0) {
                if (g == -1)
                    g = count[i];
                else
                    g = gcd(g, count[i]);
            }

        return g >= 2;
    }
    int gcd(int x, int y) {
        return x == 0 ? y : gcd(y%x, x);
    }
};
```
