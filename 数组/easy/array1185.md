# leetcode 一周中的第几天

## 解法一

基姆拉尔森公式

```go
func dayOfTheWeek(day int, month int, year int) string {
    result := map[int]string {
        0:"Sunday",
        1:"Monday",
        2:"Tuesday",
        3:"Wednesday",
        4:"Thursday",
        5:"Friday",
        6:"Saturday",
    }
    if month == 1 || month == 2 {
        month += 12
        year--
    }
	iWeek := (day+2*month+3*(month+1)/5+year+year/4-year/100+year/400)%7     
    return result[(iWeek + 1) % 7]
}
```


## 解法二


手动计算，以1971年1月1日作为基准

```go
func dayOfTheWeek(day int, month int, year int) string {
    result := map[int]string {
        0:"Sunday",
        1:"Monday",
        2:"Tuesday",
        3:"Wednesday",
        4:"Thursday",
        5:"Friday",
        6:"Saturday",
    }
    dayKey := [13]int{0,31,28,31,30,31,30,31,31,30,31,30,31}
    sum := 4
    if year != 1971 {
        for i := 1971; i < year; i++ {
            sum += dayNumber(i)
        }
    }
    if dayNumber(year) == 366 {
        dayKey[2] = 29
    }
    for i := 1; i < month; i++ {
        sum += dayKey[i]
    }
    sum += day
    ans := result[sum % 7]
    return ans
}
func dayNumber (year int) int {
    if year % 4 == 0 && year % 100 != 0 || year % 400 == 0 {
        return 366
    }
    return 365
}
```