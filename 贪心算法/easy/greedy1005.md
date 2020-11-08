# leetcode K次取反后最大化的数组和

## 解法一

```go
func largestSumAfterKNegations(A []int, K int) int {
    sort.Ints(A)
    i := 0
    for K > 0 && i < len(A) {
        if A[i] == 0 {
            K = 0
        }
        if A[i] > 0 {
            if K % 2 == 0 {
                K = 0
            }else {
                if i > 0 && A[i - 1] < A[i] {
                    A[i - 1] = -A[i - 1]
                }else {
                    A[i] = -A[i]
                }
                K = 0
            }
        }else if A[i] < 0 {
            A[i] = -A[i]
            K--
            i++
        }
    }
    sum := 0
    for _,v := range A {
        sum += v
    }
    return sum
}
```