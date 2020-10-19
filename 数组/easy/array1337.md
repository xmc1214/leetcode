# leetcode 方阵中战斗力最弱的k行

## 解法一

```go
func kWeakestRows(mat [][]int, k int) []int {
    result := make(map[int]int)
    cnt := 0
    for i := range mat {
        cnt = 0
        for j := range mat[i] {
            if mat[i][j] == 1 {
                cnt++
            }else {
                break
            }
        }
        result[i] = cnt
    }
    temp := mapsortByValue(result)
    ans := make([]int,k)
    i := 0
    for key,_ := range temp {
        if i >= k {
            break
        }
        ans[i] = temp[key].key
        i++
    }
    return ans
}
func mapsortByValue(m map[int]int) PairList {
    p := make(PairList,len(m))
    i := 0
    for k,v := range m {
        p[i] = Pair{k,v}
        i++
    }
    sort.Sort(p)
    return p
}
type Pair struct {
    key,value int
}
type PairList []Pair

func (p PairList) Len() int {return len(p)}
func (p PairList) Less(i,j int) bool {
    return p[i].value < p[j].value || (p[i].value == p[j].value && p[i].key < p[j].key)
}
func (p PairList) Swap(i,j int) {
    p[i],p[j] = p[j],p[i]
}
```

## 解法二

```go
func kWeakestRows(mat [][]int, k int) []int {
	row := len(mat)
	col := len(mat[0])
	n := make(NodeList,col + 1)
	p := make(NodeLinkList,col + 1)
	cnt := 0
	for i := 0; i < row; i++ {
		cnt = 0
		for j := 0; j < col; j++ {
			if mat[i][j] == 0 {
				break
			}
			cnt++
		}
		if p[cnt] != nil {
			(*p[cnt]).val = i
			(*p[cnt]).next = &Node{0,nil}
			p[cnt] = (*p[cnt]).next
		}else {
			n[cnt].val = i
			n[cnt].next = &Node{0,nil}
			p[cnt] = n[cnt].next
		}
	}
	j := 0
	t := 0
	ans := make([]int,k)
	for j < k {
		for n[t].next != nil {
			ans[j] = n[t].val
			j++
			if j == k {
				return ans
			}
			n[t] = *n[t].next
		}
		t++
	}
	return ans
}

type Node struct {
	val int
	next *Node
}
type NodeList []Node
type NodeLinkList []*Node
```