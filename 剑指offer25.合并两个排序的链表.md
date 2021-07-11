## 题目描述
输入两个递增排序的链表，合并这两个链表并使新链表中的节点仍然是递增排序的。
## 示例
```
输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4
```
## 代码：思想和快速排序类似
```
class Solution:
    def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
        if l1 == None:
            return l2
        if l2 == None:
            return l1
        head = ListNode(0)
        p = head
        while l1 != None and l2 != None:
            if l1.val <= l2.val:
                p.next = ListNode(l1.val)
                p = p.next
                l1 = l1.next
            else:
                p.next = ListNode(l2.val)
                p = p.next
                l2 = l2.next
        if l1 == None:
            while l2:
                p.next = ListNode(l2.val)
                p = p.next
                l2 = l2.next
        if l2 == None:
            while l1:
                p.next = ListNode(l1.val)
                p = p.next
                l1 = l1.next
        return head.next
```