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

## 解法二

相较于解法一空间复杂度由O(n ^ 2)优化成了O(n)

```go
func minimumTotal(triangle [][]int) int {
    n := len(triangle)
    f := [2][]int{}
    for i := 0; i < 2; i++ {
        f[i] = make([]int, n)
    }
    f[0][0] = triangle[0][0]
    for i := 1; i < n; i++ {
        curr := i % 2
        prev := 1 - curr
        f[curr][0] = f[prev][0] + triangle[i][0]
        for j := 1; j < i; j++ {
            f[curr][j] = min(f[prev][j - 1], f[prev][j]) + triangle[i][j]
        }
        f[curr][i] = f[prev][i - 1] + triangle[i][i]
    }
    ans := math.MaxInt32
    for i := 0; i < n; i++ {
        ans = min(ans, f[(n-1)%2][i])
    }
    return ans
}

func min(x, y int) int {
    if x < y {
        return x
    }
    return y
}
```