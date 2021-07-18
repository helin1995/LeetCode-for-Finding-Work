## 题目描述
从上到下打印出二叉树的每个节点，同一层的节点按照从左到右的顺序打印。

 

例如:
给定二叉树: [3,9,20,null,null,15,7]如下：
```
    3
   / \
  9  20
    /  \
   15   7
```

返回：
```
[3,9,20,15,7]
```

## 代码
二叉树的宽度优先遍历或者叫层序遍历：准备一个队列，现将根节点加入队列中，然后从队列中
弹出一个节点，打印当前节点的值，然后依次添加该节点的左节点、右节点（如果节点存在的话）。
重复上述过程，直到队列为空。

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def levelOrder(self, root: TreeNode) -> List[int]:
        if root == None:
            return []
        deque = [root]
        res = []
        while deque:
            cur = deque.pop(0)
            res.append(cur.val)
            if cur.left:
                deque.append(cur.left)
            if cur.right:
                deque.append(cur.right)
        return res
```