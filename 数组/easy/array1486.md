# leetcode 数组的异或操作

## 解法一

```go
func xorOperation(n int, start int) int {
    sum := 0
    for i := 0; i < n; i++ {
        temp := start + 2 * i
        sum ^= temp
    }
    return sum
}
```

## 解法二

```go
func xorOperation(n int, start int) int {
    if (start & 3) < 2 {
        if (n & 1) == 0 {
            return n & 3
        } else {
            return start + 2 * n - 3 + (n & 3)
        }
    } else {
        if (n & 1) == 0 {
            return (start + (n - 1) * 2) ^ (start - 2 + (n & 3))
        } else {
            return start + 1 - (n & 3)
        }
    }
}

```