# leetcode 有多少个小于当前数字的数字

## 解法一

暴力法模拟
```go
func smallerNumbersThanCurrent(nums []int) []int {
    len := len(nums)
    result := make([]int,len)
    cnt := 0
    for i := 0; i < len; i++ {
        cnt = 0
        for j := 0; j < len; j++ {
            if nums[j] < nums[i] && i != j {
                cnt++
            }
        }
        result[i] = cnt
    }
    return result
}
```

## 解法二

使用排序 + map 映射有效减少比较次数
```go
func smallerNumbersThanCurrent(nums []int) []int {
    len := len(nums)
     m := make(map[int]int)
     result := make([]int,len)
     copy(result,nums)
     sort.Ints(nums)
     for i := 0; i < len; i++ {
         if i == 0 {
             m[nums[i]] = 0
             continue
         }
         if nums[i] != nums[i - 1] {
             m[nums[i]] = i
         }else {
             m[nums[i]] = m[nums[i - 1]]
         }
     }
     for i := 0; i < len; i++ {
         result[i] = m[result[i]]
     }
     return result
}
```