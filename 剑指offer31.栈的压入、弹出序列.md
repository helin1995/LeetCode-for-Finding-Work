## 题目描述
输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否为该栈的弹出顺序。
假设压入栈的所有数字均不相等。例如，序列 {1,2,3,4,5} 是某栈的压栈序列，序列
{4,5,3,2,1} 是该压栈序列对应的一个弹出序列，但 {4,3,5,1,2} 就不可能是该压栈序列
的弹出序列。

## 示例1
```
输入：pushed = [1,2,3,4,5], popped = [4,5,3,2,1]
输出：true
解释：我们可以按以下顺序执行：
push(1), push(2), push(3), push(4), pop() -> 4,
push(5), pop() -> 5, pop() -> 3, pop() -> 2, pop() -> 1
```

## 示例2
```
输入：pushed = [1,2,3,4,5], popped = [4,3,5,1,2]
输出：false
解释：1 不能在 2 之前弹出。
```

## 思路
我们可以根据栈的压入序列模拟栈的压入过程，我们依次将压入序列中的元素压入辅助栈中，
同时，压入一个元素，我们就判断一下此时辅助栈顶的元素是否和弹出序列的第一个元素相等。
如果相等，那么就将辅助栈顶的元素弹出，同时将弹出序列的第一个元素删除。然后我们在比较
此时辅助栈顶和弹出序列第一个元素是否相等，方法同上。如果此时辅助栈顶元素和弹出序列
第一个元素不相等，那么我们就看压入序列是否还有值，如果还有值，则压入一个元素到辅助栈；
然后进行前面的判断；如果没有值了，那么可以直接返回false。

## 代码
```
class Solution:
    def validateStackSequences(self, pushed: List[int], popped: List[int]) -> bool:
        if pushed == []:
            return True
        stack = []
        while popped != []:
            if stack == []:
                stack.append(pushed.pop(0))
            if stack[-1] == popped[0]:
                stack.pop()
                popped.pop(0)
            else:
                if pushed == []:
                    return False
                else:
                    stack.append(pushed.pop(0))
        return True
```
