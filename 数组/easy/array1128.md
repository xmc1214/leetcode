# leetcode 多米诺骨牌对的数量

## 解法一

```go
func numEquivDominoPairs(dominoes [][]int) int {
    if len(dominoes) == 0 || len(dominoes[0]) == 0 {
        return 0
    }
    cnt := 0
    key := 0
    record := make(map[int]int)
    for i := range dominoes {
        if dominoes[i][0] < dominoes[i][1] {
            key = dominoes[i][0] * 10 + dominoes[i][1]
        }else {
            key = dominoes[i][1] * 10 + dominoes[i][0]
        }
        record[key] += 1
    }

    for _,v := range record {
        cnt += v * (v - 1) / 2
    }
    return cnt
}
```