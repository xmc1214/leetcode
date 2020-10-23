# leetcode 重新排列数组

## 解法一

使用一个新的数组接收重新排列后的元素

```
func shuffle(nums []int, n int) []int {
    len := len(nums)
    flag := 0
    ans := make([]int,len)
    for i,j := 0,n; i < n && j < len; i,j = i + 1,j + 1 {
        ans[flag] = nums[i]
        ans[flag + 1] = nums[j]
        flag += 2
    }
    return ans
}
```