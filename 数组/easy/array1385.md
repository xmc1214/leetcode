# leetcode 两个数组之间的距离值

## 解法一

```go
func findTheDistanceValue(arr1 []int, arr2 []int, d int) int {
	sort.Ints(arr2)
	count := 0
outter:
	for _, num := range arr1 {
		low := 0
		high := len(arr2) - 1
		for low <= high {
			mid := (low + high) / 2
			if arr2[mid] == num {
				continue outter
			} else if arr2[mid] > num {
				high = mid - 1
			} else {
				low = mid + 1
			}
		}
		if (low >= len(arr2) || arr2[low]-num > d || num-arr2[low] > d) && (low <= 0 || arr2[low-1]-num > d || num-arr2[low-1] > d) {
			count++
		}
	}
	return count
}
```

## 解法二

```go
func findTheDistanceValue(arr1 []int, arr2 []int, d int) int {
    m := make(map[int]Node)
    ans := 0
    for _,v := range arr2 {
        m[v] = Node{v + d,v - d}
    }
    for _,v := range arr1 {
        flag := true
        for _,val := range m {
            if val.y <= v && val.x >= v {
                flag = false
                break
            }
        }
        if flag {
            ans++
        }
    }
    return ans
}
type Node struct {
    x,y int
}
```

## 解法三

```go
func findTheDistanceValue(arr1 []int, arr2 []int, d int) int {
    if len(arr2) == 0 {
        return 0
    }

    result := 0
    for _, v := range arr1 {
        ok := true
        for _, _v := range arr2 {
            if v - _v <= d && v - _v >= -d {
                ok = false
                break
            }
        }
        if ok {
            result++
        }
    }
    return result
}
```