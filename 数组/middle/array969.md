# leetcode 煎饼排序

## 解法一

每次找出最大值将最大值通过煎饼反转移至数组最前面，在进行一次长度为数组长度的煎饼翻转将最大元素移至最后

```
func pancakeSort(A []int) []int {
	var res []int
	for k:=len(A);k>=1;k--{
		for i,v:=range A{
            //利用下标寻找最大值，排除每一次的最大值在最后面的位置
			if v==k&&i!=k-1{
                //如果最大值在数组头部则只需要一次煎饼排序
				if i!=0{
					reverse(A[:i+1])
					res=append(res,i+1)
				}
				reverse(A[:k])
				res=append(res,k)
			}
		}
	}
	return res
}

func reverse(arr []int)  {
	i,j:=0,len(arr)-1
	for i<j {
		arr[i],arr[j]=arr[j],arr[i]
		i++
		j--
	}
}
```