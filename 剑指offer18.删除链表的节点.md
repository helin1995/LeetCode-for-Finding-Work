## 题目描述
给定单向链表的头指针和一个要删除的节点的值，定义一个函数删除该节点。

返回删除后的链表的头节点。
## 示例1
```
输入: head = [4,5,1,9], val = 5
输出: [4,1,9]
解释: 给定你链表中值为5的第二个节点，那么在调用了你的函数之后，该链表应变为 4 -> 1 -> 9.
```
## 示例2
```
输入: head = [4,5,1,9], val = 1
输出: [4,5,9]
解释: 给定你链表中值为1的第三个节点，那么在调用了你的函数之后，该链表应变为 4 -> 5 -> 9.
```
## 注意
对于链表类的题目，可以设置一个哑节点（dummy node），并且它的下一个节点是头结点，这样可以使得
对原链表操作时，如果需要删除原链表的头结点，那么最后只需要返回dummy.next即为新链表。
## 代码
```
class Solution:
    def deleteNode(self, head: ListNode, val: int) -> ListNode:
        if head == None:
            return head
        dummy = ListNode(123456)
        dummy.next = head
        last, p = dummy, head
        while p:
            if p.val == val:
                last.next = p.next
                break
            else:
                p = p.next
                last = last.next
        return dummy.next
```