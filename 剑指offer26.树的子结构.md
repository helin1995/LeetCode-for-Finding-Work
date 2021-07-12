## 题目描述
输入两棵二叉树A和B，判断B是不是A的子结构。(约定空树不是任意一个树的子结构)

B是A的子结构， 即 A中有出现和B相同的结构和节点值。

例如:
给定的树 A:

           3
          / \
         4   5
        / \
       1   2
给定的树 B：

      4
     /
    1

返回 true，因为 B 与 A 的一个子树拥有相同的结构和节点值。
## 示例1
```
输入：A = [1,2,3], B = [3,1]
输出：false
```
## 示例2
```
输入：A = [3,4,5,1,2], B = [4,1]
输出：true
```
## 思路
首先，在A中找到一个和B树根节点值相同的节点，然后将A树中以该节点为根节点的树与B树
进行比较，判断B树是否是该树的子结构。
## 代码
```
class Solution:
    def isSubStructure(self, A: TreeNode, B: TreeNode) -> bool:
        if B == None:
            return False
        def preOrder(root, subTree):
            if root == None:
                return False
            if root.val == subTree.val:
                res = check(root, subTree)
                if res:
                    return True
            left = preOrder(root.left, subTree)
            right = preOrder(root.right, subTree)
            return left or right
        
        def check(root, subTree):
            if subTree == None:
                return True
            if root == None:
                return False
            if root.val == subTree.val:
                return check(root.left, subTree.left) and check(root.right, subTree.right)
            else:
                return False
        return preOrder(A, B)
```