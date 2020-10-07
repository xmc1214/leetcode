# leetcode 第k个缺失的整数

## 解法一

直接线性遍历数组使用额外的一个变量进行对比

```go
func findKthPositive(arr []int, k int) int {
	key := 0
	len := len(arr)
	for i,j := 0,1; i < len; {
		if arr[i] != j {
			key++
			if key == k {
				return j
			}
			j++
		}else {
			i++
			j++
		}
	}
	return arr[len - 1] + k - key
}
```