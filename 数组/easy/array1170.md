# leetcode 比较字符串最小字母出现频次

## 解法一

计算出两个数组每个字符串的最小字母出现频次，找出query数组中每一个频次小于word数组中元素的个数

```
func numSmallerByFrequency(queries []string, words []string) []int {
    a1 := make([]int,0)
    a2 := make([]int,0)
    searchMinval(queries,&a1)
    searchMinval(words,&a2)
    ans := make([]int,0)
    sort.Ints(a2)
    len := len(a2)
    for i := range a1 {
        for j := 0; j <= len; j++ {
            if j == len {
                ans = append(ans,0)
                continue
            }
            if a1[i] < a2[j] {
                ans = append(ans,len - j)
                break
            }
        }
    }
    return ans
}

func searchMinval(arr []string, result *[]int) {
    for _,v := range arr {
        minVal := v[0]
        m := make(map[byte]int)
        for _,val := range []byte(v) {
            if val < minVal {
                minVal = val
            }
            m[val]++
        }
        *result = append(*result,m[minVal])
    }
}
```

## 解法二

对找出最小频次方法进行优化以及后续计数方法优化

```
func numSmallerByFrequency(queries []string, words []string) []int {
	wordsFnNum := [11]int{}
	for _, word := range words {
		wordsFnNum[_numSmallerByFrequency(word)]++
	}
	var result = make([]int, len(queries), len(queries))
	for index, query := range queries {
		n := _numSmallerByFrequency(query)
		for cnt, val := range wordsFnNum {
			if n < cnt {
				result[index] += val
			}
		}
	}

	return result
}

// 找到每个字符串的最小char的频次
func _numSmallerByFrequency(str string) int {
	var dict = [26]int{}
	for _, r := range str {
		dict[r-'a'] += 1
	}

	for _, v := range dict {
		if v > 0 {
			return v
		}
	}
	return 0
}
```

## 解法三

将双重循环计数改为两层单循环计数

```
func numSmallerByFrequency(queries []string, words []string) []int {
	wordsFnNum := [12]int{}
	for _, word := range words {
		wordsFnNum[_numSmallerByFrequency(word)]++
	}
	var result = make([]int, len(queries), len(queries))
    for i := 10; i >= 0; i-- {
        wordsFnNum[i] += wordsFnNum[i + 1]
    }
	for index, query := range queries {
		n := _numSmallerByFrequency(query)
        result[index] = wordsFnNum[n + 1]
	}

	return result
}

// 找到每个字符串的最小char的频次
func _numSmallerByFrequency(str string) int {
	var dict = [26]int{}
	for _, r := range str {
		dict[r-'a'] += 1
	}

	for _, v := range dict {
		if v > 0 {
			return v
		}
	}
	return 0
}
```