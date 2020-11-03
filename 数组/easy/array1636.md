# leetcode 按照频率将数组升序

## 解法一

```go
func frequencySort(nums []int) []int {
	var numss []numSort
	sortMap := make(map[int]int)
	var res []int
	for _, v := range nums {
		sortMap[v]++
	}
	for k, v := range sortMap {
		numss = append(numss, numSort{value:k, fre:v})
	}
	sort.Sort(numSilce(numss))
	for _, v := range numss {
		for i := 0; i <v.fre; i++ {
			res = append(res, v.value)
		}
	}
	return res
}
type numSort struct {
	value int
	fre  int
}

type numSilce []numSort


func (p numSilce) Len() int           { return len(p) }
func (p numSilce) Less(i, j int) bool {
	if p[i].fre != p[j].fre {
		return p[i].fre < p[j].fre
	}
	return p[i].value >p[j].value
}
func (p numSilce) Swap(i, j int)      { p[i], p[j] = p[j], p[i] }
```

## 解法二

```go
func frequencySort(nums []int) []int {
    m := make(map[int]int)
    for _,v := range nums {
        m[v]++
    }
    for i := 0; i < len(nums); i++ {
        for j := 0; j < len(nums) - i - 1; j++ {
            if m[nums[j + 1]] < m[nums[j]] {
                nums[j + 1],nums[j] = nums[j],nums[j + 1]
            }else if  m[nums[j + 1]] == m[nums[j]] {
                if nums[j + 1] > nums[j] {
                    nums[j + 1],nums[j] = nums[j],nums[j + 1]
                }
            }
        }
    }
    return nums
}
```