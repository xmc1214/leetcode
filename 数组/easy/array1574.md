# leetcode 统计好三元组

## 解法一

三重暴力循环

```go
func countGoodTriplets(arr []int, a int, b int, c int) int {
    len := len(arr)
    result := 0
    if len < 3 {
        return result
    }
    for i := 0; i < len; i++ {
        for j := i + 1; j < len; j++ {
            if (int)(math.Abs(float64(arr[i] - arr[j]))) <= a {
                for k := j + 1; k < len; k++ {
                    if(int)(math.Abs(float64(arr[j] - arr[k]))) <= b {
                        if (int)(math.Abs(float64(arr[i] - arr[k])) )<= c {
                            result++
                        }
                    }else {
                        continue
                    }
                }
            }else {
                continue
            }
        }
    }
    return result
}
```

## 解法二

利用频次数组前缀和优化

```go
func countGoodTriplets(arr []int, a int, b int, c int) int {
    len := len(arr)
    result := 0
    if len < 3 {
        return result
    }
    sum := make([]int,1001)
    for j := 0; j < len; j++ {
            for k := j + 1; k < len; k++ {
                if(int)(math.Abs(float64(arr[j] - arr[k]))) <= b{
                    lj := arr[j] - a
                    lk := arr[j] + a
                    rj := arr[k] - c
                    rk := arr[k] + c
                    l,r := 0,0
                    if lj > rj {
                        l = lj
                    }else {
                        l = rj
                    }
                    if l < 0 {
                        l = 0
                    }
                   if lk < rk {
                       r = lk
                   }else {
                       r = rk
                   }
                   if r > 1000 {
                       r = 1000
                   }
                    if l <= r {
                        if l == 0 {
                            result += sum[r]
                        }else {
                            result += sum[r] - sum[l - 1]
                        }
                    }
            }
        }
        for t := arr[j]; t <= 1000; t++ {
            sum[t]++
        }
    }
    return result
}
```