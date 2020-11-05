# leetcode 在排序数组中查找数字

## 解法一

```go
func search(nums []int, target int) int {
    ans := 0
    left,right := 0,len(nums) - 1
    pos := -1
    for left <= right {
        mid := left + (right - left) / 2
        if nums[mid] < target {
            left = mid + 1
        }
        if nums[mid] > target {
            right = mid - 1
        }
        if nums[mid] == target {
            pos = mid
            ans++
            break
        }
    }
    if pos == -1 {
        return 0
    }
    i,j := pos - 1,pos + 1
    for i >= 0 || j < len(nums) {
        if i >= 0 {
            if nums[i] == target {
                ans++
                i--
            }else{
                i = -1
            }
        }
        if j < len(nums) {
            if nums[j] == target {
                ans++
                j++
            }else {
                j = len(nums)
            }
        }
    }
    return ans
}
```


## 解法二


```go
func search(nums []int, target int) int {
    var search func(target int) int
    search = func(target int) int {
        left,right := 0,len(nums) - 1
        for left <= right {
            mid := left + (right - left) / 2
            if nums[mid] <= target {
                left = mid + 1
            }else {
                right = mid - 1
            }
        }
        return right
    }
    return search(target) - search(target - 1)
}
```