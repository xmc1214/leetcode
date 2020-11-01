# leetcode 矩阵中的幸运数字

## 解法一

找出每一行最小数字对比该数字所在列的最大数字是否相同

```go
func luckyNumbers (matrix [][]int) []int {
    ans := make([]int,0)
    row,col := len(matrix),len(matrix[0])
    for i := 0; i < row; i++ {
        j := 0
        keyRow := 0
        rowMinVal := math.MaxInt32
        for j < col {
            if rowMinVal > matrix[i][j] {
                rowMinVal = matrix[i][j]
                keyRow = j
            }
            j++
        }
        colMaxVal := math.MinInt32
        t := 0
        for t < row {
            if colMaxVal < matrix[t][keyRow] {
                colMaxVal = matrix[t][keyRow]
            }
            t++
        }
        if rowMinVal == colMaxVal {
            ans = append(ans,rowMinVal)
        }
    }
    return ans
}
```