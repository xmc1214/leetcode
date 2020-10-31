# leetcode 找出幸运数

## 解法一

使用数组下标记录元素出现次数，对比下标和出现次数是否相等

```go
func findLucky(arr []int) int {
    ans := -1
    m := make([]int,501)
    for _,v := range arr {
        m[v]++
    }
    for i,v := range m {
        if v > 0{
            if i == v && v > ans {
                ans = v
            }
        }
    }
    return ans
}
```