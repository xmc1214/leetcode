# leetcode 奇数值单元格的数目

## 解法一

```go
func oddCells(n int, m int, indices [][]int) int {
    ans := 0
    m1 := make(map[int]int)
    m2 := make(map[int]int)
    for _,v := range indices {
        if _,ok := m1[v[0]]; !ok {
            m1[v[0]] = 1
        }else {
            m1[v[0]]++
        }
        if _,ok := m2[v[1]]; !ok {
            m2[v[1]] = 1
        }else {
            m2[v[1]]++
        }
    }
    for i := 0; i < n; i++ {
        temp := m1[i] % 2
        for j := 0; j < m; j++ {
            if temp == 0 && m2[j] % 2 > 0 {
                ans++
            }
            if temp > 0 && m2[j] % 2 == 0 {
                ans++
            }
        }
    }
    return ans
}
```