# leetcode 岛屿的周长

## 解法一

遍历每一个节点判断是否为岛屿，若是则计算四周情况，否则跳过

```go
var dx = []int {0,1,0,-1}
var dy = []int {1,0,-1,0}

func islandPerimeter(grid [][]int) int {
    ans := 0
    for i := range grid {
        for j := range grid[i] {
            if grid[i][j] == 1 {
                ans += 4
                for t := 0; t < 4; t++ {
                    x := i + dx[t]
                    y := j + dy[t]
                    if x >= 0 && x < len(grid) && y >= 0 && y < len(grid[i]) {
                        if grid[x][y] == 1 {
                            ans--
                        }
                    }
                }
            }
        }
    }
    return ans
}

```