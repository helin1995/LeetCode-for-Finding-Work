## 题目描述
输入一棵二叉树和一个整数，打印出二叉树中节点值的和为输入整数的所有路径。从
树的根节点开始往下一直到叶节点所经过的节点形成一条路径。

示例:
给定如下二叉树，以及目标和target = 22，
```
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1
```

返回：
```
[
   [5,4,11,2],
   [5,8,4,5]
]
```
## 方法: 深度优先遍历+回溯
## 代码：
```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def pathSum(self, root: TreeNode, target: int) -> List[List[int]]:
        if not root:
            return []
        res, temp = [], []
        def preOrder(root, target):
            if not root:
                return
            target -= root.val
            temp.append(root.val)
            if target == 0 and root.left == None and root.right == None:
                res.append(temp[:])
            preOrder(root.left, target)
            preOrder(root.right, target)
            temp.pop()
        preOrder(root, target)
        return res
```