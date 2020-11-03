# leetcode 两个数组的交集

## 解法一

```go
func intersection(nums1 []int, nums2 []int) []int {
    ans := make([]int,0)
    m := make(map[int]int)
    for _,v := range nums1 {
        if m[v] == 0 {
            m[v]++
        }
    }
    for _,v := range nums2 {
        if m[v] > 0 {
            m[v]--
            ans = append(ans,v)
        }
    }
    
    return ans
}
```