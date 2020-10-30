# leetcode 数组中的重复数字

## 解法一

简单哈希表查找

```
func findRepeatNumber(nums []int) int {
    temp := make(map[int]int)
    ans := 0
    for _,v := range nums {
        if temp[v] != 0 {
            ans = v
            break
        }
        temp[v]++
    }
    return ans
}
```

## 解法二

利用索引值和数组中的值一一对应，而重复的元素会发生索引冲突

```
func findRepeatNumber(nums []int) int {
    for i := 0; i < len(nums); i++ {
        for i != nums[i] {
            if nums[i] == nums[nums[i]] {
                return nums[i]
            }
            nums[i], nums[nums[i]] = nums[nums[i]], nums[i]
        }
    }
    return -1
}
```