# leetcode 汇总区间

## 解法一

```go
func summaryRanges(nums []int) []string {
    len := len(nums)
    result := make([]string,0)
    if len < 1 {
        return result
    }
    if len == 1 {
        result = append(result,strconv.Itoa(nums[0]))
        return result
    }
    for i,j := 0,0; i < len; i++ {
        if i + 1 < len && nums[i + 1] - nums[i] == 1 {
            continue
        }
        if i == j {
            result = append(result,strconv.Itoa(nums[j]))
        }else {
            result = append(result,strconv.Itoa(nums[j]) + "->" + strconv.Itoa(nums[i]))
        }
        j = i + 1
    }
    return result
}
```