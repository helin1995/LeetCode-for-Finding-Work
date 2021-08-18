## 题目描述
请实现 copyRandomList 函数，复制一个复杂链表。在复杂链表中，每个节点除了
有一个 next 指针指向下一个节点，还有一个 random 指针指向链表中的任意节点
或者 null。

## 思路
用一个哈希表保存原始节点和对应新节点的映射

## 代码
```
class Solution:
    def copyRandomList(self, head: 'Node') -> 'Node':
        if not head:
            return None
        p = head
        dic = {}  # 原节点：新节点
        dummy = Node(0)
        p1 = dummy
        while p:
            p1.next = Node(p.val)
            dic[p] = p1.next
            p1 = p1.next
            p = p.next
        p = dummy.next
        while p and head:
            if head.random == None:
                p.random = None
            else:
                p.random = dic[head.random]
            p = p.next
            head = head.next
        return dummy.next
```