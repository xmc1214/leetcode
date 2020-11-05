# leetcode 删除某些元素后的数组均值

## 解法一

```go
func trimMean(arr []int) float64 {
    sort.Ints(arr)
    len := len(arr)
    start,end := len * 5 / 100, len - len * 5 / 100
    temp := 0
    for i := start; i < end; i++ {
        temp += arr[i]
    }
    ans := float64(temp) / float64(end - start)
    return ans
}
```