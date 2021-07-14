## 题目描述
定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的 min 函数在该栈中，调
用 min、push 及 pop 的时间复杂度都是 O(1)。
## 示例
```
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.min();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.min();   --> 返回 -2.
```
## 思路
这道题难点在于要使得找到栈中最小值的复杂度为O(1)，我们可以利用一个辅助栈，这个辅助栈
是用来存放当前栈中最小值。将某个元素压入栈中时，也要将压入这个元素之后栈中的最下角元素
添加到这个辅助栈中；弹出栈顶元素时，同时弹出栈和辅助栈的栈顶元素。
```
class MinStack:

    def __init__(self):
        """
        initialize your data structure here.
        """
        self.data = []  # 存放栈中的元素
        self.min_val = []  # 按照入栈顺序存放当前栈中的最小值


    def push(self, x: int) -> None:
        """
        压栈：将x压入栈中
        """
        self.data.append(x)
        if len(self.data) == 1:
            self.min_val.append(x)
        else:
            self.min_val.append(min(x, self.min_val[-1]))



    def pop(self) -> None:
        """
        将栈顶元素弹出
        """
        self.data.pop()
        self.min_val.pop()


    def top(self) -> int:
        """
        返回栈顶元素
        """
        return self.data[-1]


    def min(self) -> int:
        """
        返回栈中值最小的元素
        """
        return self.min_val[-1]



# Your MinStack object will be instantiated and called as such:
# obj = MinStack()
# obj.push(x)
# obj.pop()
# param_3 = obj.top()
# param_4 = obj.min()
```