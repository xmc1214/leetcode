# leetcode 单词搜索

## 解法一

此解法是我自己写的dfs，在剪枝和判断条件方面不是最优，有些判断比较多余

```go
var dx = [4]int{0,1,0,-1}
var dy = [4]int{1,0,-1,0}

func exist(board [][]byte, word string) bool {
	ans := false
	res := make([]byte,0)
	maz := make([][]bool,len(board))
	for i := range maz {
		maz[i] = make([]bool,len(board[0]))
	}
	for i := range board {
		for j := range board[i] {
			if board[i][j] == word[0] {
				maz[i][j] = true
				res = append(res,board[i][j])
				if dfs(board,word,res,maz,Node{i,j},1) {
					ans = true
					break
				}
				for i := range maz {
					maz[i] = make([]bool,len(board[0]))
				}
				res = make([]byte,0)
			}
		}
		if ans {
			break
		}
	}
	return ans
}

func dfs(board [][]byte,word string, res []byte, maz [][]bool, n Node,step int) bool {
	if step == len(word) {
		if string(res[:]) == word {
			return true
		}
		return false
	}
	for i := 0; i < 4; i++ {
		x := n.x + dx[i]
		y := n.y + dy[i]
		if !check(board,x,y,maz) {
			continue
		}
		if board[x][y] == word[step] {
			res = append(res,board[x][y])
			maz[x][y] = true
			if dfs(board,word,res,maz,Node{x,y},step + 1) {
				return true
			}
			res = res[:len(res) - 1]
            maz[x][y] = false
		}
	}
	return false
}

func check(board[][]byte,x,y int,maz [][]bool) bool {
	return x >= 0 && x < len(board) && y >= 0 && y < len(board[0]) && !maz[x][y]
}

type Node struct {
	x,y int
}
```

## 解法二

此解法是在解法一的基础上去掉了一些不必要的判断条件，以及在搜索的方式上进行了改进

```go
var dx = [4]int{0,1,0,-1}
var dy = [4]int{1,0,-1,0}

func exist(board [][]byte, word string) bool {
	ans := false
	maz := make([][]bool,len(board))
	for i := range maz {
		maz[i] = make([]bool,len(board[0]))
	}
	for i := range board {
		for j := range board[i] {
			if dfs(board,word,maz,i,j,0) {
				ans = true
				break
			}
		}
		if ans {
			break
		}
	}
	return ans
}

func dfs(board [][]byte,word string,maz [][]bool,px,py int,step int) bool {
	if board[px][py] != word[step] {
		return false
	}
	if step == len(word) - 1 {
		return true
	}
	maz[px][py] = true
	defer func() {maz[px][py] = false}()
	for i := 0; i < 4; i++ {
		x := px + dx[i]
		y := py + dy[i]
		if !check(board,x,y,maz) {
			continue
		}
		if dfs(board,word,maz,x,y,step + 1) {
			return true
		}
	}
	return false
}

func check(board[][]byte,x,y int,maz [][]bool) bool {
	return x >= 0 && x < len(board) && y >= 0 && y < len(board[0]) && !maz[x][y]
}
```