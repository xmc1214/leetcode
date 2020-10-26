# leetcode 商品折扣后的最终价格

## 解法一

简单模拟，但是当数据量足够大后会超出时间限制

```go
func finalPrices(prices []int) []int {
    len := len(prices)
    for i := range prices {
        j := i + 1
        for ; j < len; j++ {
            if prices[j] <= prices[i] {
                prices[i] -= prices[j]
                break
            }
        }
    }
    return prices
}
```

## 解法二

使用单调递增栈找出第一个小于该元素的元素

```go
//找到元素右边第一个比他小的数，顺序，单调增栈
func finalPrices(prices []int) []int {
	stack := make([]int, 0)
	for i := 0; i < len(prices); i++ {
		for len(stack) > 0 && prices[i] <= prices[stack[len(stack)-1]] {
			pop := stack[len(stack)-1]
			stack = stack[:len(stack)-1]
			prices[pop] -= prices[i]
		}
		stack = append(stack, i)
	}
	return prices
}
```