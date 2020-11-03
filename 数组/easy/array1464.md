# leetcode 数组中最大元素乘积

## 解法一

```go
func maxProduct(nums []int) int {
    sort.Ints(nums)
    ans := 0
    ans = (nums[len(nums) - 1] - 1) * (nums[len(nums) - 2] - 1)
    return ans
}
```