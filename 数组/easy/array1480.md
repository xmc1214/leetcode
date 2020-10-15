# leetcode 一维数组的动态求和

## 解法一

简单模拟

```go
func runningSum(nums []int) []int {
    temp := 0
    for i := range nums {
        temp += nums[i]
       nums[i] = temp
    }
    return nums
}
```