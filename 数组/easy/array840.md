# leetcode 数组类 矩阵中的幻方

## 解法一

遍历查找符合条件的九宫格,注意题目中规定的是1～9不同的数字,这一条件增加了很多约束,条件判断函数中首先遍历九宫格判断中心位置是否为5,是否出现重复数字,再次遍历九宫格判断行之和,列之和,对角线之和是否等于15

```c++
class Solution {
public:
    bool valid(const vector<vector<int>>& grid, int r, int c) {
        if (grid[r + 1][c + 1] != 5) return false;
        unordered_set<int> s;
        for (int i = 0; i < 3; ++i) {
            for (int j = 0; j < 3; ++j) {
                int t = grid[r + i][c + j];
                if (t < 1 || t > 9 || s.count(t)) return false;
                s.insert(t);
            }
        }
        for (int i = 0; i < 3; ++i) {
            int s1 = 0;
            int s2 = 0;
            for (int j = 0; j < 3; ++j) {
                s1 += grid[r + i][c + j];
                s2 += grid[r + j][c + i];
            }
            if (s1 != 15 || s2 != 15) return false;
        }
        // 以上判断已经足够断定幻方是否存在
        return true;
    }
    int numMagicSquaresInside(vector<vector<int>>& grid) {
        if (grid.empty()) return 0;
        int R = grid.size();
        int C = grid[0].size();
        int res = 0;
        for (int i = 0; i < R - 2; ++i) {
            for (int j = 0; j < C - 2; ++j) {
                res += valid(grid, i, j);
            }
        }
        return res;
    }
};
```
