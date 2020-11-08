# leetcode 模拟行走的机器人

## 解法一

```go
func robotSim(commands []int, obstacles [][]int) int {
    m := make(map[Node]int)
    dx := [4]int{0,1,0,-1}
    dy := [4]int{1,0,-1,0}
    x,y,di := 0,0,0
    ans := 0
    for _,v := range obstacles {
        m[Node{v[0],v[1]}]++
    }
    for _,v := range commands {
        if v == -2 {
            di = (di + 3) % 4
        }else if v == -1 {
            di = (di + 1) % 4
        }else {
            for i := 0; i < v; i++ {
                nx := x + dx[di]
                ny := y + dy[di]
                if m[Node{nx,ny}] > 0 {
                    break
                }
                x = nx
                y = ny
                ans = max(ans, x * x + y * y)
            }
        }
    }
    return ans
}

func max(i,j int) int {
    if i > j {
        return i
    }
    return j
}
type Node struct {
    x,y int
}
```