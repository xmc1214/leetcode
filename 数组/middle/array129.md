# leetcode 求根到叶子节点的数字之和

## 解法一

利用递归遍历二叉树，在遍历时使用temp将每个节点的数字记录成字符串，当遍历到叶子节点后可以将temp加入结果数组,最后计算结果数组的和

```
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func sumNumbers(root *TreeNode) int {
    ans := []string{}
    var temp = ""
    travel(root,&ans,temp)
    res := 0
    for i := range ans {
        val,_ := strconv.Atoi(ans[i])
        res += val
    }
    return res
}

func travel(root *TreeNode,ans *[]string,temp string) *TreeNode {
    if root == nil {
        return nil
    }
    temp += strconv.Itoa(root.Val)
    travel(root.Left,ans,temp)
    travel(root.Right,ans,temp)
    // 此处要注意遍历到叶子节点才加入temp,要排除遍历完二叉树后再次加入根节点的情况
    if root.Left == nil && root.Right == nil {
        *ans = append(*ans,temp)
    }
    return root
}
```