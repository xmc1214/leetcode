# leetcode 按键持续时间最长的键

## 解法一

```go
func slowestKey(releaseTimes []int, keysPressed string) byte {
    maxVal := math.MinInt32
    var ans byte
    for i := range []byte(keysPressed) {
        temp := 0
        if i == 0 {
            temp = releaseTimes[0]
        }else {
            temp = releaseTimes[i] - releaseTimes[i - 1]
        }
        if temp > maxVal {
            maxVal = temp
            ans = keysPressed[i]
        }else if temp == maxVal {
            ans = maxByte(ans,keysPressed[i])
        }
    }
    return ans
}
func maxByte(i,j byte) byte {
    if i > j {
        return i
    }
    return j
}
```