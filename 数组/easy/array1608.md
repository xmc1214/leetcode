# leetcode 特殊数组的特征值

## 解法一

先将数组升序，然后利用下标i代替特征值x,当 i != len(nums)时需要判断是否有i个元素大于等于i
,当 i == len(nums)时只需判断第一个元素是否大于等于i即可

```go
func specialArray(nums []int) int {
    sort.Ints(nums)
    result := -1
    len := len(nums)
    for i := 1; i <= len; i++ {
        if i == len {
            if nums[0] >= i {
                result = i
            }
        }else {
            if nums[len - i - 1] < i && nums[len - i] >= i {
                result = i
            }
        }
    }
    return result
}
```