# leetcode 和为0的N个唯一整数

## 解法一

主要判断一下n的奇偶性，如果为奇数则需要一个0去调和，其他的就按照对称性一正一负相加即可

```go
func sumZero(n int) []int {
    ans := make([]int,n)
    i := 0
    if n % 2 != 0 {
        ans[0] = 0
        n--
        i = 1
    }
    n /= 2
    for n > 0 {
        ans[i] = n
        ans[i + 1] = (-1) * n
        n--
        i += 2
    }
    return ans
}
```