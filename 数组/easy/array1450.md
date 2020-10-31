# leetcode 在限定时间内做作业的学生人数

## 解法一

简单条件判断

```go
func busyStudent(startTime []int, endTime []int, queryTime int) int {
    ans := 0
    for i := 0; i < len(startTime); i++ {
        if startTime[i] <= queryTime && endTime[i] >= queryTime {
            ans++
        }
    }
    return ans
}
```