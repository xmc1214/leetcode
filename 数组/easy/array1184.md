# leetcode 公交站间的距离

## 解法一

同时计算两个方向的路程，选取更小路程

```
func distanceBetweenBusStops(distance []int, start int, destination int) int {
    l,r := 0,0
    ans := 0
    if start > destination {
        destination,start = start,destination
    }
    for i := destination; i > start; i-- {
        l += distance[i - 1]
    }
    for j := destination;; j++ {
        if j >= len(distance) && j % len(distance) >= start {
            break
        }
        r += distance[j % len(distance)]
    }
    if l < r {
        ans = l
    }else {
        ans = r
    }
    return ans
}
```