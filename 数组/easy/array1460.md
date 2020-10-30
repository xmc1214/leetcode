# leetcode 通过翻转使两个数组相等

## 解法一

使用内部排序让两个数组升序，对比两个数组是不是一样

```
func canBeEqual(target []int, arr []int) bool {
    sort.Ints(target)
    sort.Ints(arr)
    for i := range target {
        if target[i] != arr[i] {
            return false
        }
    }
    return true
}
```

## 解法二

使用map记录target数组的元素，再比较arr数组元素是不是和map记录的一样

```
func canBeEqual(target []int, arr []int) bool {
    m := make(map[int]int)
    for _,v := range target {
        m[v]++
    }
    for _,v := range arr {
        if m[v] == 0 {
            return false
        }
        m[v]--
    }
    return true
}
```