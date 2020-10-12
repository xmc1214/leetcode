# leetcode 绝对差不超过限制的最长连续子数组

## 解法一

此解法比较次数有重复，对于一部分测试用例会超出时间限制
```go
func longestSubarray(nums []int, limit int) int {
	cnt := 0
	i,j := 0,0
	ans := 0
	len := len(nums)
	min,max := 0,0
	for i < len {
		cnt = 0
		if nums[i] - nums[i] <= limit {
			cnt++
		}
		min,max = nums[i],nums[i]
		j = i + 1
		for j < len {
			if nums[j] > max {
				max = nums[j]
			}
			if nums[j] < min {
				min = nums[j]
			}
			if max - min > limit {
				break
			}else {
				cnt++
				j++
			}
		}
		ans = (int)(math.Max(float64(ans),float64(cnt)))
		i++
	}
	return ans
}
```

## 解法二
使用滑动窗口+单向队列减少遍历次数
```go
type Queue []int

func (q Queue)front()int{
    return q[0]
}

func (q Queue)lastpop()Queue{
    return q[:len(q)-1]
}

func (q Queue)last() int{
    return q[len(q)-1]
}

func (q Queue)frontpop()Queue{
    return q[1:]
}

func (q Queue)nonempty()bool{
    return len(q)!=0
}

func max(a,b int)int{
    if a>=b{
        return a
    }
    return b
}


func longestSubarray(nums []int, limit int) int {
    Max,Min:=make(Queue,0),make(Queue,0)
    left,ans:=0,0
    for i,v:=range nums{
        for Max.nonempty()&&nums[Max.last()]<=v{
            Max=Max.lastpop()
        }
        Max=append(Max,i);
        for Min.nonempty()&&nums[Min.last()]>=v{
            Min=Min.lastpop()
        }
        Min=append(Min,i);

        for Max.nonempty()&&Min.nonempty()&&nums[Max.front()]-nums[Min.front()]>limit{
            if Min.front()<=left{
                Min=Min.frontpop()
            }
            if Max.front()<=left{
                Max=Max.frontpop()
            }
            left++
        }
        ans=max(ans,i-left+1)
    }
    return ans;
}
```