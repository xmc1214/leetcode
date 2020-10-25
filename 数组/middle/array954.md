# leetcode 二倍对数组

## 解法一

使用map记录每个元素的个数,将数组升序，从较小值开始检查该元素的两倍值是否存在，每存在一对都需要在map中减去相应次数，当ans等于数组长度一半时返回true,否则遍历完后返回false

```go
func canReorderDoubled(A []int) bool {
    m := make(map[int]int)
    for i := range A {
        m[A[i]]++
    }
    ans := 0
    len := len(A)
    if len == 0 {
        return true
    }
    sort.Ints(A)
    for j := range A {
        if m[A[j]] > 0 {
            if m[2 * A[j]] > 0 {
                ans++
                m[2 * A[j]]--
                m[A[j]]--
            }
        }
        if ans == len / 2 {
            return true
        }
    }
    return false
}
```