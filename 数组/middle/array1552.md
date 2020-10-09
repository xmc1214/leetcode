# leetcode 两球之间的磁力

## 解法一

关键词:数学推导,二分查找

```go
func maxDistance(position []int, m int) int {
	sort.Ints(position)
	left,right,mid := 1,position[len(position) - 1],0
	ans := -1
	for left <= right {
		mid = (left + right) / 2
		if check(mid,position,m) {
			ans = mid
			left = mid + 1
		}else {
			right = mid - 1
		}
	}
	return ans
}

func check(x int, position []int, m int) bool{
	pre := position[0]
	cnt := 1
	for i := 1; i < len(position); i++ {
		if position[i] - pre >= x {
			pre = position[i]
			cnt++
		}
	}
	return cnt >= m
}
```