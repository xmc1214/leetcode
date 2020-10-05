# leetcode 访问所有点的最小距离

## 解法一

此题适用于切比雪夫距离解答，两个坐标之间的最短距离是横坐标之差和纵坐标之差间的最大值

```go
func minTimeToVisitAllPoints(points [][]int) int {
	len := len(points)
	result := 0
        dx,dy := 0.0,0.0
	for i := 1; i < len; i++ {
        dx = math.Abs(float64(points[i][0] - points[i - 1][0]))
        dy = math.Abs(float64(points[i][1] - points[i - 1][1]))
        result += (int)(math.Max(dx,dy))
    }
	return result
}
```