# leetcode 柠檬水找零

## 解法一

```go
func lemonadeChange(bills []int) bool {
    var (numOfFive,numOfTen,numOfTwenty int)
    for _,v := range bills {
        v -= 5
        if v == 0 {
            numOfFive++
        }
        if v == 5 {
            numOfFive--
            if numOfFive < 0 {
                return false
            }
            numOfTen++
        }
        if v == 15 {
           if numOfTen != 0 {
               v -= 10
               numOfTen--
           }
            numOfFive -= v / 5
            if numOfFive < 0 {
                return false
            }
            numOfTwenty++
        }
    }
    return true
}
```