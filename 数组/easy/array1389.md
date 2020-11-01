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

## 解法二

```go
package main

func createTargetArray(nums []int, index []int) []int {
	var res = make([]int, len(nums))
	for k, i := range index {
		copy(res[i+1:], res[i:])
		res[i] = nums[k]
	}
	return res
}`
```

## 解法三

手动移动元素

```go
package main

func createTargetArray(nums []int, index []int) []int {
	var res = make([]int, len(nums))
	for i,v := range index {
        for t := len(res) - 1; t > v; t-- {
            res[t] = res[t - 1]
        }
        res[v] = nums[i]
	}
	return res
}
```