# leetcode 去掉工资中的最低工资和最高工资后的平均工资

## 解法一

简单模拟，利用内部排序找出最低和最高工资，求和后减去两个工资数再求平均工资

```
func average(salary []int) float64 {
    sort.Ints(salary)
    max := salary[len(salary) - 1]
    min := salary[0]
    sum := 0
    for i := range salary {
        sum += salary[i]
    }
    sum -= (min + max)
    average := float64(sum) / float64(len(salary) - 2)
    return average
}
```