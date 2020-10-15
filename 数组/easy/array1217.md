# leetcode 玩筹码

## 解法一

理解题意后只要找出在奇数位置元素个数和偶数位置元素个数后，找出更小的那个将元素移至另一个位置即可

```
func minCostToMoveChips(position []int) int {
    len := len(position)
    result := 0
    if len <= 1 {
        return result
    }
    odd,even := 0,0
    for i := range position {
        if position[i] & 1 == 1 {
            odd++
        }else {
            even++
        }
    }
    result = min(odd,even)
    return result
}
func min(i,j int) int {
    if i < j {
        return i
    }
    return j
}
```