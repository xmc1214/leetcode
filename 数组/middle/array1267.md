# leetcode 统计参与通信的服务器

## 解法一

使用两个哈希表分别存储每行每列服务器数量，再遍历二维数组的每个位置如果该位置有服务器且该行或者该列的服务器数量大于一台则互相通信的服务器数量加一

```go
func countServers(grid [][]int) int {
    row := make(map[int]int)
    col := make(map[int]int)
    ans := 0
    for i,value := range grid {
        for j := range value {
            if grid[i][j] == 1 {
                row[i]++
                col[j]++
            }
        }
    }
    for i,value := range grid {
        for j := range value {
            if grid[i][j] != 0 && (row[i] > 1 || col[j] > 1) {
                ans++
            }
        }
    }
    return ans
}
```