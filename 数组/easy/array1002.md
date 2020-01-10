# leetcode 数组类 查找常用字符

## 解法一

统计每个单词内26个字母出现的次数存入数组,将次数最小的放在第一行数组

```c++
class Solution {
public:
    vector<string> commonChars(vector<string>& A) {
        vector<string> out;
        int num[100][26]={0};                  //建立一个二维数组，标记所有出现的字母次数
        for(int i =0;i<A.size() ;i++)
            for(int j=0;j<A[i].size();j++)
                num[i][(A[i][j]-'a')]++;

        for(int j=0;j<26;j++)                  //将所有列的最小值存到第一行
            for(int i=1;i<A.size();i++)
                num[0][j] = min (num[0][j],num[i][j]);

        string str;                           //按照第一行保存的次数输出相应字母
        for(int i=0;i<26;i++){
            while(num[0][i]--)
            {
                str.clear();
                str.push_back((char)('a'+i));
                out.push_back(str);
            }
        }
        return out;
    }
};
```
