## 题目描述
请实现一个函数按照之字形顺序打印二叉树，即第一行按照从左到右的顺序打印，第二层按照
从右到左的顺序打印，第三行再按照从左到右的顺序打印，其他行以此类推。


例如:
给定二叉树:[3,9,20,null,null,15,7],
```
    3
   / \
  9  20
    /  \
   15   7
```

返回其层次遍历结果：
```
[
  [3],
  [20,9],
  [15,7]
]
```

## 思路：层序遍历 + 双端队列，代码如下：
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
        deque = collections.deque([root])
        res = []
        while deque:
            temp = []
            # 打印奇数层，从左往右
            for _ in range(len(deque)):
                node = deque.popleft()
                temp.append(node.val)
                if node.left:
                    deque.append(node.left)
                if node.right:
                    deque.append(node.right)
            res.append(temp)
            if not deque:
                break
            temp = []
            # 打印偶数层，从右往左
            for _ in range(len(deque)):
                node = deque.pop()
                temp.append(node.val)
                if node.right:
                    deque.appendleft(node.right)
                if node.left:
                    deque.appendleft(node.left)
            res.append(temp)
        return res
```
