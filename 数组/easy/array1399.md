# leetcode 统计最大组数目

## 解法一

```go
func countLargestGroup(n int) int {
    record := [37]int{}
    maxVal,cnt := math.MinInt32,0
    for i := 1; i <= n; i++ {
        temp := i
        val := 0
        for temp > 0 {
            val += temp % 10
            temp /= 10
        }
        record[val]++
        if record[val] > maxVal {
            cnt = 1
            maxVal = record[val]
        }else if record[val] == maxVal {
            cnt++
        }
    }
    return cnt
}
```