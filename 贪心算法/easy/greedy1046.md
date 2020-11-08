# leetcode 最后一块石头的重量

## 解法一

```go
func lastStoneWeight(stones []int) int {
    sort.Ints(stones)
    cnt := 0
    for len(stones) > 1 {
        cnt = len(stones) - 1
        if stones[cnt] > stones[cnt - 1] {
            temp := stones[cnt] - stones[cnt - 1]
            stones = append(stones[:cnt - 1],temp)
        }else {
            stones = stones[:cnt - 1]
        }
        sort.Ints(stones)
    }
    if len(stones) == 0 {
        return 0
    }
    return stones[0]
}
```