# leetcode 子矩阵的查询

## 解法一

此题只要考察对于语法的熟悉度,按要求实现即可

```go
type SubrectangleQueries struct {
	rectangle [][]int
}


func Constructor(rectangle [][]int) SubrectangleQueries {
	subrectangleQueries := SubrectangleQueries{rectangle: rectangle}
	return subrectangleQueries
}


func (this *SubrectangleQueries) UpdateSubrectangle(row1 int, col1 int, row2 int, col2 int, newValue int)  {
	for i := row1; i <= row2; i++ {
		for j := col1; j <= col2; j++ {
			this.rectangle[i][j] = newValue
		}
	}
}

func (this *SubrectangleQueries) GetValue(row int, col int) int {
	return this.rectangle[row][col]
}
```