# leetcode 使数组唯一的最小增量

## 解法一

排序，然后遍历数组，当前元素大小小于等于前一个元素时，将当前元素换为前一个元素加一，操作数相应加上

```
func minIncrementForUnique(A []int) int {
    cnt := 0
    len := len(A)
    sort.Ints(A)
    for i:= 1; i < len; i++ {
        if A[i] <= A[i - 1] {
            pre := A[i]
            A[i] = A[i - 1] + 1
            cnt += A[i] - pre
        }
    }
    return cnt
}
```

## 解法二

计数排序，使用额外的数组存储每一个元素的次数，然后保持每一个位置的个数为一，多的往后移，计算移动次数

```
func minIncrementForUnique(A []int) int {
  counter := [40001]int{}
  ans := 0
  maxVal := -1
  for i := range A {
      counter[A[i]]++
      maxVal = max(maxVal,A[i])
  }
  for j := 0; j <= maxVal; j++{
      if counter[j] > 1 {
          d := counter[j] - 1
          ans += d
          counter[j + 1] += d
      }
  }
  d := counter[maxVal + 1] - 1
  ans += (1 + d) * d / 2
  return ans
}
func max(i,j int) int {
    if i < j {
        return j
    }
    return i
}
```

## 解法三

线性探测+路径压缩

比如 [3, 2, 1, 2, 1, 7] 就映射成了 [3, 2, 1, 4, 5, 7]。

我想了下，这道题目其实和解决 hash 冲突的线性探测法比较相似！
如果地址冲突了，会探测它的下一个位置，如果下一个位置还是冲突，继续向后看，直到第一个不冲突的位置为止。

关键点：因为直接线性探测可能会由于冲突导致反复探测耗时太长，因此我们可以考虑探测的过程中进行路径压缩。
怎么路径压缩呢？就是经过某条路径最终探测到一个空位置 x 后，将这条路径上的值都变成空位置所在的下标 x，那么假如下次探测的点又是这条路径上的点，则可以直接跳转到这次探测到的空位置 x，从 x 开始继续探测。


```
func minIncrementForUnique(A []int) int {
    counter := [80000]int{}
    for i := range counter {
        counter[i] = -1
    }
    ans := 0
    for i := range A {
        cnt := findPos(A[i],&counter)
        ans += cnt - A[i]
    }
    return ans
}

func findPos(i int, counter *[80000]int) int {
    temp := (*counter)[i]
    if temp == -1 {
        (*counter)[i] = i
        return i
    }
    temp = findPos(temp + 1,counter)
    (*counter)[i] = temp
    return temp
}
```