# leetcode 买卖股票的最佳时机 II

## 解法一

```go
func maxProfit(prices []int) int {
    res := 0
    for i := 1; i < len(prices); i++ {
        res += max(0, prices[i] - prices[i - 1]);
    }
    return res
}
func max(i,j int) int {
    if i > j {
        return i
    }
    return j
}
```