# leetcode 最小绝对差

## 解法一

遍历数组，一边寻找最小的绝对差值，一边将符合条件的数组加入集合，当找到更小的绝对差时就清空集合并重新将符合条件的数组加入集合

```go
func minimumAbsDifference(arr []int) [][]int {
	sort.Ints(arr)
	result := make([][]int,0)
	len := len(arr)
	minVal := math.MaxInt32
	for i := 0; i < len - 1; i++ {
		if arr[i + 1] - arr[i] > minVal {
			continue
		}
		if arr[i + 1] - arr[i] < minVal {
			result = result[:0]
			minVal = arr[i + 1] - arr[i]

		}
		result = append(result,[]int{arr[i],arr[i + 1]})
	}
	return result
}
```