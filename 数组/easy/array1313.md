# leetcode 解压缩编码列表

## 解法一

直接按照题目意思模拟元素加入新数组的过程即可

```go
func decompressRLElist(nums []int) []int {
    var result []int
    freq,val,j := 0,0,0
    for i := 0; i < len(nums) / 2; i++ {
        freq = nums[2 * i]
        val = nums[2 * i + 1]
        for freq > 0 {
            result = append(result,val)
            j++
            freq--
        }
    }
    return result
}
```