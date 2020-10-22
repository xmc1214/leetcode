# leetcode 删除最短子数组使剩余数组有序

## 解法一

    //双指针
	//
	//先找出最大有序前缀和最大有序后缀 的长度 pre和suf
	//如果pre==n则代表全部有序
	//上述为预处理 及 排除特殊场景
	//
	//前缀指针i和后缀指针j, i从0开始，j从后缀的起点开始
	//如果arr[j]>=arr[j],则代表i前的和j后的可形成升序，计算值并和min比较，
	//   然后前缀指针i右移，选择更大的值进一步比较；
	//如果arr[j]<arr[i],则代表j的值过小，后缀指针右移,直到能形成升序
	//	
	//补充：前缀指针i的作用是缩小距离，后缀指针j的作用是用来形成升序

```
func findLengthOfShortestSubarray(arr []int) int {
	n := len(arr)
	if n <= 1 {
		return 0
	}

	//前缀升序长度
	pre := 1
	for i := 1; i < n && arr[i] >= arr[i-1]; i++ {
		pre++
	}
	//全部升序
	if pre == n {
		return 0
	}

	//后缀升序长度
	suf := 1
	for i := n - 1; i > 0 && arr[i] >= arr[i-1]; i-- {
		suf++
	}

	//只选择前缀或者后缀 需删除的最小数量
	min := n - pre
	if n-suf < min {
		min = n - suf
	}

	//后缀指针j初始化一次，之后只右移
	j := n - suf
	for i := 0; i < pre; i++ {
		for ; j < n; j++ {
			//如果可形成升序，计算最小值，移动前缀指针i（用来缩小min）
			if arr[j] >= arr[i] {
				if j-i-1 < min {
					min = j - i - 1
				}
				break
			}
		}
	}

	return min
}
```