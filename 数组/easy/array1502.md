# leetcode 判断是否能形成等差数列

## 解法一

```go
func canMakeArithmeticProgression(arr []int) bool {
    sort.Ints(arr)
    if len(arr) <= 2 {
        return true
    }
    for i := 1; i < len(arr) - 1; i++ {
        if arr[i] - arr[i - 1] != arr[i + 1] - arr[i] {
            return false
        }
    }
    return true
}
```