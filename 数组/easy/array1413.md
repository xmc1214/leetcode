# leetcode 逐步求和得到正数的最小值

## 解法一

简单贪心

```go
func minStartValue(nums []int) int {
    minVal := 0
    if nums[0] <= 0 {
        minVal = 1 - nums[0]
    }else {
        minVal = 1
    }
    sum := minVal
    for i := 0; i < len(nums); i++ {
        sum += nums[i]
        if sum < 1 {
            minVal += 1 - sum
            sum = 1
        }
    }
    return minVal
}
```