# leetcode 好数对的数目

## 解法一

```go
func numIdenticalPairs(nums []int) int {
    m := make(map[int]int)
    ans := 0
    for _,v := range nums {
        m[v]++
    }
    for _,v := range m {
        ans += v * (v - 1) / 2
    }
    return ans
}
```