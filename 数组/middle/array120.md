# leetcode 三角形最小路径和

## 解法一

```go
func minimumTotal(triangle [][]int) int {
	row := len(triangle)
	f := make([][]int,row)
    for i := 0; i < row; i++ {
        f[i] = make([]int,row)
    }
    f[0][0] = triangle[0][0]
    for j := 1; j < row; j++ {
        f[j][0] = f[j - 1][0] + triangle[j][0]
        for t := 1; t < j; t++ {
            f[j][t] = min(f[j - 1][t],f[j - 1][t - 1]) + triangle[j][t]
        }
        f[j][j] = f[j - 1][j - 1] + triangle[j][j]
    }
    ans := math.MaxInt32
    for i := 0; i < row; i++ {
        ans = min(ans,f[row - 1][i])
    }
    return ans
}

func min(i,j int) int {
    if i < j {
        return i
    }
    return j
}
```