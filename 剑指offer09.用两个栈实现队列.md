## 题目描述
用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和
在队列头部删除整数的功能。(若队列中没有元素，deleteHead操作返回 -1 )
## 示例1
```
输入：
["CQueue","appendTail","deleteHead","deleteHead"]
[[],[3],[],[]]
输出：[null,null,3,-1]
```
## 示例2
```
输入：
["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]
[[],[],[5],[2],[],[]]
输出：[null,-1,null,null,5,2]
```

## 思路
声明两个栈stack1和stack2，对于appendTail操作，就将value压入stack1中。那么对于deleteHead操作，肯定不能从stack1中
弹出value，因为此时stack1是后进先出。所以我们就要利用stack2，对于deleteHead操作来说，我们将stack1中元素依次弹出，
然后依次压入stack2中。此时stack2中，栈顶的元素是最先进队列的或者说最先进stack1的。那么，弹出stack2的时候就是先进先出
的结果了。具体实现如下代码。
## 代码
```
class CQueue:
    def __init__(self):
        from queue import LifoQueue
        self.stack1 = LifoQueue()
        self.stack2 = LifoQueue()

    def appendTail(self, value: int) -> None:
        self.stack1.put(value)

    def deleteHead(self) -> int:
        if self.stack2.empty():
            if self.stack1.empty():
                return -1
            else:
                while not self.stack1.empty():
                    self.stack2.put(self.stack1.get())
        return self.stack2.get()
```
上述代码中，我们加载了python中的LifoQueue模块，这个模块就是实现栈的。但是，这个模块时间效率很低。因此采用数组来
代替栈，这样时间效率要比上述代码高。代码如下。
```
class CQueue:
    def __init__(self):
        self.stack1 = []
        self.stack2 = []

    def appendTail(self, value: int) -> None:
        self.stack1.append(value)

    def deleteHead(self) -> int:
        if self.stack2 == []:
            if self.stack1 == []:
                return -1
            else:
                while self.stack1 != []:
                    self.stack2.append(self.stack1.pop())
        return self.stack2.pop()
```