## 题目描述
从上到下按层打印二叉树，同一层的节点按从左到右的顺序打印，每一层打印到一行。

 

例如:
给定二叉树: [3,9,20,null,null,15,7]，如下：
```
    3
   / \
  9  20
    /  \
   15   7
```

返回其层次遍历结果
```
[
  [3],
  [9,20],
  [15,7]
]
```
## 代码
```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
        if root == None:
            return []
        res, layer, deque = [], [], [root]  # 最终的结果、每一层的结果、队列
        cur_level = 1  # 当前节点所在的层
        hash_table = {root: 1}  # 节点以及其所在的层数
        while deque:
            cur = deque.pop(0)
            level = hash_table[cur]
            if level == cur_level:
                layer.append(cur.val)
            else:
                res.append(layer)
                layer = []
                layer.append(cur.val)
                cur_level = level
            if cur.left:
                deque.append(cur.left)
                hash_table[cur.left] = cur_level + 1
            if cur.right:
                deque.append(cur.right)
                hash_table[cur.right] = cur_level + 1
        res.append(layer)
        return res
```