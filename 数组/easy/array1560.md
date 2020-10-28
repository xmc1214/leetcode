# leetcode 圆形赛道上经过最多的次数

## 解法一

简单过程模拟

```go
func mostVisited(n int, rounds []int) []int {
	m := make([]int,101)
	len := len(rounds)
	maxVal := math.MinInt32
	for i := 0; i < len - 1; i++ {
		temp := rounds[i]
		m[temp]++
		maxVal = max(maxVal,m[temp])
		temp++
		for temp < rounds[i + 1] || (temp > rounds[i + 1] && temp <=n) || (temp > n && (temp % n) < rounds[i + 1]) {
			if temp <= n {
				m[temp]++
				maxVal = max(maxVal,m[temp])
			}else {
				m[temp % n]++
				maxVal = max(maxVal,m[temp % n])
			}
			temp++
		}
	}
	m[rounds[len - 1]]++
	maxVal = max(maxVal,m[rounds[len - 1]])
	ans := make([]int,0)
	for i,v := range m {
		if v == maxVal {
			ans = append(ans,i)
		}
	}
	return ans
}
func max(i,j int) int {
	if i < j {
		return j
	}
	return i
}
```