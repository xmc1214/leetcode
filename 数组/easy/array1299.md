# leetcode 将每个元素替换为右侧最大元素

## 解法一

每次从新的切片中找出最大元素替换当前数组元素，当遍历到最后一个元素时直接替换为-1,最后返回原数组

```go
func replaceElements(arr []int) []int {
    var temp []int
	for index := range arr{
		if index + 1 <= len(arr) - 1 {
			temp = arr[index + 1:]
			arr[index] = findMax(temp)
		}else {
			arr[index] = -1
		}

	}
	return arr
}
func findMax(arr []int) int {
	maxVal := -1
	for i := range arr{
		if arr[i] > maxVal {
			maxVal = arr[i]
		}
	}
	return maxVal
}
```

## 解法二

从后往前遍历数组，i记录下标，当 `i==len(arr) - 1`时将数组元素作为max的初始化值，并将数组元素替换为-1,使用temp记录当前数组元素,
并将数组元素替换为max,比较temp和max的大小并更新max的值

```go
func replaceElements(arr []int) []int {
    max := 0
    for i := len(arr) - 1; i >= 0; i--{
        if i == len(arr) - 1 {
            max = arr[i]
            arr[i] = -1
        }else {
            temp := arr[i]
            arr[i] = max
            if temp > max {
                max = temp
            }
        }
    }
	return arr
}
```