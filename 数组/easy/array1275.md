# leetcode 找出井字棋游戏获胜者

## 解法一

```
func tictactoe(moves [][]int) string {
    a,b := 0,0
    len := len(moves)
    temp := []int{7,56,73,84,146,273,292,448}
    var result string
    if len < 5 {
        result = "Pending"
        return result
    }
    for i := 0; i < len; i++ {
        cur := 1 << (3 * moves[i][0]+ moves[i][1])
        if i & 1 == 1 {
            b ^= cur
        }else {
            a ^= cur
        }
        for _,val := range temp {
            if b & val == val {
                result = "B"
                return result
            }
            if a & val == val {
                result = "A"
                return result
            }
        }
    }
    if len != 9 {
        result = "Pending"
    }else {
        result = "Draw"
    }
    return result
}
```