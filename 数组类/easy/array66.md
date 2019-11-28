# leetcode 数组类 加一

## 解法一

此处考虑到测试数据比较大不能采用先还原出原数字进行加一操作后再存入数组,根据对数组元素进位判断直接在原数组中修改数字。特殊情况是需要考虑进位问题

```c++
class Solution
{
 public:
 vector<int> plusOne(vector<int>& digits){
  for(int i = digits.size() - 1; i >= 0; i--)
    {
      digits[i]++;
      digits[i] = digits[i] % 10;
      if(digits[i] != 0)
      {
        return digits;
      }
    }
   digits.insert(digits.begin(),1);
   return digits;
  }
};
```
