# leetcode 二维网格的迁移

## 解法一

三重暴力循环，重新计算每个数组元素的位置，每次将新的数组覆盖旧的数组

```go
func shiftGrid(grid [][]int, k int) [][]int {
    m := len(grid)
    n := len(grid[0])
    for ;k > 0; k-- {
        tempArr := make([][]int,m)
        for i := range tempArr {
            tempArr[i] = make([]int,n)
        }
        for row,_ := range grid {
            for col,_ := range grid[0] {
                if col == n - 1  && row == m - 1 {
                    tempArr[0][0] = grid[row][col]
                }

                if col == n - 1 && row != m - 1 {
                    tempArr[row + 1][0] = grid[row][col]
                }

                if col != n - 1 {
                    tempArr[row][col + 1] = grid[row][col]
                }
            }
        }
        grid = tempArr
    }
    return grid
}
```

## 解法二

利用数学推导直接计算出经过k次迁移后每个数组元素的位置，减少一次循环

` newCol = (col + k) % n`
` newRow = (row + (col + k) / n) % m`

```go
func shiftGrid(grid [][]int, k int) [][]int {
    m := len(grid)
    n := len(grid[0])
    tempArr := make([][]int,m)
    for i := range tempArr {
		tempArr[i] = make([]int,n)
	}
    newRow,newCol := 0,0
    for row := range grid {
        for col := range grid[row] {
            newCol = (col + k) % n
            newRow = (row + (col + k) / n) % m
            tempArr[newRow][newCol] = grid[row][col]
        }
    }
    grid = tempArr
    return grid
}
```