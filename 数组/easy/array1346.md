# leetcode 检查整数及其两倍数是否存在

## 解法一

使用map存储每个元素的两倍数，并记录元素下标，以符合i!=j的条件

```go
func checkIfExist(arr []int) bool {
    m := make(map[int]int)
    temp := 0
    for i := range arr {
        temp = arr[i] * 2
        m[temp] = i
    }
    for j := range arr {
        if v,ok := m[arr[j]]; ok {
           if v != j {
               return true
           }
        }
    }
    return false
}
```