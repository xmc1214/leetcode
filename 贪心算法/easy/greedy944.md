# leetcode 删列造序

## 解法一

```go
func minDeletionSize(A []string) int {
    ans := 0
    cnt := len(A[0])
    for i := 0; i < cnt; i++ {
        for j := 0; j < len(A) - 1; j++ {
            if A[j][i] > A[j + 1][i] {
                ans++
                break
            }
        }
    }
    return ans
}
```