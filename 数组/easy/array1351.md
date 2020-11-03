# leetcode 统计矩阵的负值数

## 解法一

```go
func countNegatives(grid [][]int) int {
    row,col := len(grid),len(grid[0])
    ans := 0
    for i := row - 1; i >= 0; i-- {
        for j := col - 1; j >=0; j-- {
            if grid[i][j] >= 0 {
                break
            }
            ans++
        }
    }
    return ans
}
```

## 解法二

```go
func countNegatives(grid [][]int) int {
    col := len(grid[0])
    ans := 0
    for i := range grid {
        left,right,pos := 0,col - 1,-1
        for left <= right {
            mid := left + (right - left) / 2
            if grid[i][mid] < 0 {
                pos = mid
                right = mid - 1
            }else {
                left = mid + 1
            }
        }
        if pos >= 0 {
            ans += col - pos
        }
    }
    return ans
}

```