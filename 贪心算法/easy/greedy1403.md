# leetcode 非递增顺序的子顺序列

## 解法一

排序 + 倒序遍历

```go
func minSubsequence(nums []int) []int {
    sort.Ints(nums)
    ans := make([]int,0)
    sum := 0
    for _,v := range nums {
        sum += v
    }
    tempVal := 0
    for i := len(nums) - 1; i >=0; i-- {
        tempVal += nums[i]
        ans = append(ans,nums[i])
        if sum - tempVal < tempVal {
            break
        }
    }
    return ans
}
```