# leetcode 能否连接形成数组

## 解法一

```go
func canFormArray(arr []int, pieces [][]int) bool {
    m := make(map[int]int)
    for i := range pieces {
        if _,ok := m[pieces[i][0]]; !ok {
            m[pieces[i][0]] = i
        }
    }
    for j := 0; j < len(arr); {
        if _,ok := m[arr[j]]; !ok {
            return false
        }
        temp := pieces[m[arr[j]]]
        for t := 0; t < len(temp);t,j = t + 1,j + 1 {
            if arr[j] != temp[t] {
                return false
            }
        }
    }
    return true
}
```