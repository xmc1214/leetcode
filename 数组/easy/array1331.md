# leetcode 数组序号转换

## 解法一

克隆一个数组，进行排序，使用hashMap记录每一个元素的下标，最后根据原数组去hashMap中寻找对应的下标

```
func arrayRankTransform(arr []int) []int {
    len := len(arr)
    temp := make([]int,len)
    copy(temp,arr)
    sort.Ints(temp)
    result := make(map[int]int)
    index := 1
    for k,v := range temp {
        if k > 0 && temp[k] != temp[k - 1] {
            result[v] = index
            index++
        }
        if k == 0 {
            result[v] = index
            index++
        }
    }
    for i := 0; i < len; i++ {
        arr[i] = result[arr[i]]
    }
    return arr
}
```