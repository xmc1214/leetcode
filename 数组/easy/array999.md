# leetcode 数组类 车的可用捕获量

## 解法一

题目的本质就是在R所在的行与列数组中查找B之前的p,由于原数组范围过大我们可以减小搜索范围,将R所在的行与列提取出来,同时去掉空白块

```c++
class Solution {
public:
    int numRookCaptures(vector<vector<char>>& board) {
      int col = board.size();
      int row = board[0].size();
      int rc = -1,rr = -1;
      for(int i = 0; i < col; i++) {
        for(int j = 0; j < row; j++) {
          if(board[i][j] == 'R') {
            rc = i;
            rr = j;
            break;
          }
        }
        if(rc != -1 && rr != -1) break;
      }
      vector<char>h;
      vector<char>l;
      int hFlag = 0,lFlag = 0;
      int hTemp = -1,lTemp = -1;
      for(int i = 0; i < col; i++)
      {
        if(board[i][rr] != '.')
        {
          hTemp++;
          if(board[i][rr] == 'R') hFlag = hTemp;
          h.push_back(board[i][rr]);
        }
      }
      for(int j = 0; j < row; j++)
      {
        if(board[rc][j] != '.')
        {
          lTemp++;
          if(board[rc][j] == 'R') lFlag = lTemp;
          l.push_back(board[rc][j]);
        }
      }
      int ans = 0;
      if(hFlag + 1 < h.size() && h[hFlag + 1] == 'p') ans++;
      if(hFlag - 1 >= 0 && h[hFlag - 1] == 'p') ans++;
      if(lFlag + 1 < l.size() && l[lFlag + 1] == 'p') ans++;
      if(lFlag - 1 >= 0 && l[lFlag - 1] == 'p') ans++;
      return ans;
    }
};
```
