# leetcode 统计数组中的偶数

## 解法一

针对本题给定的数据集有一种hack解法

```
func findNumbers(nums []int) int {
    ans := 0
    for _,v := range nums {
        if (v >= 10 && v < 100) || (v >= 1000 && v < 10000) || v == 100000 {
            ans++
        }
    }
    return ans
}
```

## 解法二

适用于全部数据的通用解法

```
func findNumbers(nums []int) int {
    ans := 0
    for _,v := range nums {
        temp := 10
        cnt := 1
        for v / temp != 0 {
            temp *= 10
            cnt++
        }
        if cnt % 2 == 0 {
            ans++
        }
    }
    return ans
}
```


## 解法三

将元素转化为字符串直接判断长度是否为偶数

```
func findNumbers(nums []int) int {
    count := 0

	for _, v := range nums {
		if len(strconv.Itoa(v))%2 == 0 {
			count++
		}
	}

	return count
}
```