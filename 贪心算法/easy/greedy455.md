# leetcode 分发饼干

## 解法一

```go
func findContentChildren(g []int, s []int) int {
    sort.Ints(g)
    sort.Ints(s)
    i,j := 0,0
    ans := 0
    for i < len(g) && j < len(s) {
        if g[i] <= s[j] {
            i++
            ans++
        }
        j++
    }
    return ans
}
```