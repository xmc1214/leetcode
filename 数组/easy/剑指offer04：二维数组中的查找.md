# leetcode 二维数组中的查找

## 解法一

直接双重循环判断目标值和数组中的元素是否相等

```go
func findNumberIn2DArray(matrix [][]int, target int) bool {
    for i := range matrix {
        for j := range matrix[0] {
            if matrix[i][j] == target {
                return true
            }
        }
    }
    return false
}
```

## 解法二

对于每一行的数组元素进行二分查找，相较于解法一而言内层循环的速度变快了

```go
func findNumberIn2DArray(matrix [][]int, target int) bool {
	rowLen := len(matrix)
    if rowLen == 0 {
        return false
    }
	colLen := len(matrix[0])
	for i := 0; i < rowLen; i++ {
		colStart,colEnd := 0,colLen - 1
		for colStart <= colEnd {
			colMid := (colStart + colEnd) / 2
			if matrix[i][colMid] == target {
				return true
			}
			if matrix[i][colMid] < target {
				colStart = colMid + 1
			}
			if matrix[i][colMid] > target {
				colEnd = colMid - 1
			}
		}
	}
	return false
}
```

## 解法三

从矩阵的右上角开始往左和往下寻找目标元素，利用矩阵的元素大小分布特点可以减少一层循环

```go
func findNumberIn2DArray(matrix [][]int, target int) bool {
	rowLen := len(matrix)
	if rowLen == 0 {
		return false
	}
	colLen := len(matrix[0])
    if colLen == 0 { 
        return false
    }
	for i,j := 0,colLen - 1; i < rowLen && j >= 0; {
        if target == matrix[i][j] {
            return true
        }
        if target < matrix[i][j] {
            j--
            continue
        }
        if target > matrix[i][j] {
            i++
        }
    }
	return false
}
```