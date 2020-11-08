# leetcode 分割平衡字符串

## 解法一

```go
func balancedStringSplit(s string) int {
    LNum,RNum := 0,0
    ans := 0
    for _,v := range s {
        if v == 'L' {
            LNum++
        }else {
            RNum++
        }
        if LNum == RNum {
            ans++
            LNum,RNum = 0,0
        }
    }
    return ans
}
```