# leetcode 重复至少k次且长度为M的模式

## 解法一

```go
func containsPattern(arr []int, m int, k int) bool {
    for i := 0; i <= len(arr) - m * k; i++ {
        offset := 0
        for offset < m * k {
            if arr[i + offset] != arr[i + offset % m] {
                break
            }
            offset++
        }
        if offset == m * k {
            return true
        }
    }
    return false
}
```