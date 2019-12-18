# leetcode 数组类 1比特与2比特字符

## 解法一

遍历数组元素,如果为1则需要下一个元素组合成2比特的数,i = i + 2,否则i = i + 1,当i>=size时判断是由i++得到还是i+2得到的就能得出结果

```c++
class Solution {
public:
 bool isOneBitCharacter(vector<int> &bits) {
  int size = bits.size();
  if (size == 0) {
    return false;
  }
  if (size == 1) {
    return bits[0] == 0;
  }
  int i = 0;
  while (i < size) {
    if (bits[i] == 1) {
      i += 2;
      if (i >= size) {
        return false;
      }
    } else {
      i++;
      if (i >= size) {
        return true;
      }
    }
  }
  return 0;
  }
};
```
