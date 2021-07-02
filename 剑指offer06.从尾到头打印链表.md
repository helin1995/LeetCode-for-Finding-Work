## 题目描述
输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。

## 示例
```
输入：head = [1,3,2]
输出：[2,3,1]
```
## 方法1
采用递归的思路，O(n)、O(n)
## 代码
```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def reversePrint(self, head: ListNode) -> List[int]:
        if head == None:
            return []
        res = []
        return self.process(head, res)

    def process(self, head, res):
        if head == None:
            return
        # res.append(head.val)  # 从头到尾添加
        self.process(head.next, res)
        res.append(head.val)    # 从尾到头添加，有点类似于二叉树的后序遍历
        return res
```

## 方法2
从头到尾遍历，添加元素，然后从尾到头输出，可以知道这个可以由栈来实现，在python中可以直接使用arr[::-1]来从尾到头
输出arr的值。O(n)、O(n)
## 代码
```
class Solution:
    def reversePrint(self, head: ListNode) -> List[int]:
        if head == None:
            return []
        res = []
        while head:
            res.append(head.val)
            head = head.next
        return res[::-1]
```