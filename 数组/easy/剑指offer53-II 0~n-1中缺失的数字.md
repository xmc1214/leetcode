# leetcode 0~n-中缺失的数字

## 解法一

线性查找,遍历数组

```go
func missingNumber(nums []int) int {
    ans := 0
    for i := range nums {
        if ans != nums[i] {
            return ans
        }
        ans++
    }
    return ans
} 
```

## 解法二

二分查找,减少对比次数

```go
func missingNumber(nums []int) int {
    left,right := 0,len(nums)
    for left < right {
        mid := left - (left - right) / 2
        if nums[mid] != mid {
            right = mid
        }else {
            left = mid + 1
        }
    }
    return left
} 
```