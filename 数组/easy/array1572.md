# leetcode 矩阵对角线元素和

## 解法一

直接使用双指针将对角线元素累加

```go
func diagonalSum(mat [][]int) int {
    row := len(mat)
    ans := 0
    for i,j := 0,row - 1; i < row && j >= 0; i,j = i + 1,j - 1 {
        ans += mat[i][i]
        if i!= j {
            ans += mat[i][j]
        }
    }
    return ans
}
```