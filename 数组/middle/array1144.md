# leetcode 递减元素使数组呈锯齿状

## 解法一

```go
func movesToMakeZigzag(nums []int) int {
        n := len(nums)
        ans1,ans2 := 0,0
        for i :=0; i < n; i++ {
            //把该位置变成比前一个小需要d1步
            d1 := 0
            if i > 0 && nums[i] >= nums[i-1] {
                d1 = nums[i] - nums[i-1] + 1
            }
            //把该位置变成比后一个小需要d2步
            d2 := 0
            if i < n-1 && nums[i] >= nums[i+1] {
                d2 = nums[i] - nums[i+1] + 1
            }
            //取max就把该位置凹下去
            //按奇偶累加
            if i % 2 == 0 {
                ans1 += max(d1, d2);
            } else {
                ans2 += max(d1, d2);
            }
        }
        //按奇偶位置凹下去需要比较少的那个方案
        return min(ans1, ans2);
}

func max(i,j int) int {
    if i > j {
        return i
    }
    return j
}

func min(i,j int) int {
    if i < j {
        return i
    }
    return j
}
```