# leetcode 按照既定顺序创建目标数组

## 解法一

理解题目后其实就是对切片的插入操作

```go
func createTargetArray(nums []int, index []int) []int {
    len := len(nums)
    ans := make([]int,0)
    for i := 0; i < len; i++ {
        ans = append(ans[:index[i]], append([]int{nums[i]}, ans[index[i]:]...)...)
    }
    return ans
}
```