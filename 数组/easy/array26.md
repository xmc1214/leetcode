# leetcode 数组类 删除数组重复项

## 解法一

利用STL中的去重容器将重复元素移至不重复元素后面再进行删除

```c++
class Solution
{
public:
 int removeDuplicates(vector<int>& nums)
 {
  auto iter = unique(nums.begin(), nums.end());   //重排容器
  nums.erase(iter, nums.end());   //删除重复元素
  return nums.size();
 }
};
```

## 解法二

利用快慢指针,慢指针为i,快指针为j,利用指针j遍历数组,当nums[j] != nums[i]时，指针i加一并使nums[i]=nums[j],否则将跳过重复项，最后返回实际长度

```c++
class Solution
{
public:
 int removeDuplicates(vector<int>& nums)
 {
        if(nums.size() == 0)
        {
            return 0;
        }
        int i = 0;
        for(int j = 1; j < nums.size(); j++)
        {
            if(nums[j] != nums[i])
            {
                i++;
                nums[i] = nums[j];
            }
        }
        return i + 1;
 }
};
```
