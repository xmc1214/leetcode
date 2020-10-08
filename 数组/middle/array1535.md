# leetcode 找出数组游戏的赢家

## 解法一

如果不考虑运行时间的限制可以直接按照题目意思模拟

```go
func getWinner(arr []int, k int) int {
    numLastWin,min,max,count := 0,0,0,0
    maxArrNum := 0
    if k >= len(arr) - 1 {
        for i := range arr {
            if maxArrNum < arr[i] {
                maxArrNum = arr[i]
            }
        }
        return maxArrNum
    }
    for count != k {
        if arr[0] > arr[1] {
            max,min = arr[0],arr[1]
        }else {
            max,min = arr[1],arr[0]
        }
        if numLastWin != max && count != 0{
            count = 1
        }else {
            count++
        }
        numLastWin = max
        arr[0] = max
        arr = append(arr,min)
        arr = append(arr[:1],arr[2:]...)
    }
    return max
}
```

## 解法二

解法一虽然可以通过全部测试用例，但是会超出时间限制，所以需要将题目中不必要的移动元素操作去掉

```go
func getWinner(arr []int, k int) int {
    numLastWin,max,count := 0,0,0
    if arr[0] > arr[1] {
            numLastWin = arr[0]
        }else {
            numLastWin = arr[1]
        }
    if k == 1 {
        return numLastWin
    }
    count = 1
    max = numLastWin
    for i := 2; i < len(arr); i++ {
        if arr[i] > numLastWin {
            numLastWin = arr[i]
            count = 1
        }else {
            count++
            if count == k {
                return max
            }
        }
        if max < numLastWin {
            max = numLastWin
        }
    }
    return max
}
```