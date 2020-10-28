# leetcode 从中序和后序遍历序列构造二叉树

## 解法一

每次从后序遍历中找出根节点，根据根节点在中序遍历序列中的位置分出左右子树，递归此过程

```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
var m = make(map[int]int)
var p []int
func buildTree(inorder []int, postorder []int) *TreeNode {
	for i := range inorder {
		m[inorder[i]] = i
	}
	n := len(postorder) - 1
	for _,v := range postorder {
		p = append(p,v)
	}
	return TreeConstructor(0,n)
}

func TreeConstructor(left,right int) *TreeNode {
	if left > right {
		return nil
	}
	rootVal := p[len(p) - 1]
	p = p[:len(p) - 1]
	root := &TreeNode{Val:rootVal}
	rootIndex := m[rootVal]
	root.Right = TreeConstructor(rootIndex + 1,right)
	root.Left = TreeConstructor(left,rootIndex - 1)
	return root
}

```