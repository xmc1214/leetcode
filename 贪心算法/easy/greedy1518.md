# leetcode 换酒问题

## 解法一

```go
func numWaterBottles(numBottles int, numExchange int) int {
    ans := 0
    if numBottles < numExchange {
        return numBottles
    }
    for numBottles >= numExchange {
        ans += numBottles - numBottles % numExchange
        numBottles = numBottles / numExchange + numBottles % numExchange
    }
    ans += numBottles
    return ans
}
```