# leetcode 数组类 删除数组重复项

## 解法一

利用迭代器it遍历数组，当数组中的值与val相等时，使用vector的erase()方法进行移除元素,将移除后返回的迭代器重新赋予it,保证it不会变成野指针,且要进行越界检查,当数组值不等于val时，it加一,最后返回nums的长度

```c++
class Solution
{
public:
 int removeElement(vector<int>& nums, int val)
 {
  for(vector<int>::iterator it = nums.begin(); it != nums.end();)
  {
   if((*it) == val)
   {
    it = nums.erase(it);
   }
  else
   {
    it++;
   }
   if(it == nums.end())
   {
    break;
   }
  }
  return nums.size();
 }
};

```

## 解法二

题目中指明元素位置可以发生改变,当数组中的元素与val相等时,将该元素与数组最后一个元素进行交换并将数组大小减一,否则跳过检查下一个元素

```c++
class Solution
{
public:
 int removeElement(vector<int>& nums, int val)
 {
  int i = 0;
  int n = nums.size();
  while(i < n)
  {
   if(nums[i] == val)
   {
    nums[i] = nums[n - 1];
    n--;
   }
   else
   {
    i++;
   }
  }
  return n;
 }
};
```
