# leetcode 数组类 合并有序数组

## 解法一

此题就是归并排序的归并部分,比较两数组中的元素,较小的元素插入新的容器并下标加一,直到其中一个数组的元素完全插入新的数组中,再将另外一个数组的剩余元素插入数组,将新数组与nums1交换元素即可,但此解法需要利用额外的空间

```c++
class Solution
{
public:
 void merge(vector<int>& nums1, int m, vector<int>& nums2, int n)
 {
  vector<int> target;
  int i = 0, j = 0;
  int temp = 0;
  while(i < m && j < n)
  {
    target.push_back(nums1[i] < nums2[j] ? nums1[i++] : nums2[j++]);
    temp++;
  }
  target.resize(m + n);
  if(i >= m)
  {
    copy(nums2.begin() + j,nums2.begin() + n,target.begin() + temp);
  }
  else
  {
    copy(nums1.begin() + i,nums1.begin() + m,target.begin() + temp);
  }
  nums1 = target;
 }
};
```

## 解法二

直接将nums2的元素插入nums1末尾,再排序,此解法时间复杂度比较高

```c++
class Solution
{
public:
 void merge(vector<int>& nums1, int m, vector<int>& nums2, int n)
 {
  int len = m + n;
  for (int i : nums2) nums1[m++] = i;
  sort(nums1.begin(), nums1.begin() + len);
 }
};
```
