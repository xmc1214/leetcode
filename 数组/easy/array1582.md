# leetcode 二进制矩阵中的特殊位置

## 解法一

```go
func numSpecial(mat [][]int) int {
    row,col := len(mat),len(mat[0])
    rowMap,colMap := make(map[int]int),make(map[int]int)
    ans := 0
    for i := 0; i < row; i++ {
        for j := 0; j < col; j++ {
            rowMap[i] += mat[i][j]
            colMap[j] += mat[i][j]
        }
    }
    for i,v := range mat {
        for _i,_v := range v {
            if _v == 1 {
                if rowMap[i] == 1&& colMap[_i] == 1{
                    ans++
                }
            }
        }
    }
    return ans
}
```