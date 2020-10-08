# leetcode 缀点成线

## 解法一

数学思想，利用两点间的斜率判断是否在一条直线，但需要解决分母为零,即斜率不存在的情况,所以采用乘积的方式判断

```go
func checkStraightLine(coordinates [][]int) bool {
    len := len(coordinates)
    if len == 2 {
        return true
    }
    valX := coordinates[1][0] - coordinates[0][0]
    valY := coordinates[1][1] - coordinates[0][1]
    tempX,tempY := 0,0
    for i := 2; i < len; i++ {
        tempX = coordinates[i][0] - coordinates[i - 1][0]
        tempY = coordinates[i][1] - coordinates[i - 1][1]
        if valX * tempY != valY * tempX {
            return false
        }
    }
    return true
}
```