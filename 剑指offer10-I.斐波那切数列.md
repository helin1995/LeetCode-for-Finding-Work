## 题目描述
写一个函数，输入 n ，求斐波那契（Fibonacci）数列的第 n 项（即 F(N)）。斐波那契数
列的定义如下：
```
F(0) = 0,   F(1) = 1
F(N) = F(N - 1) + F(N - 2), 其中 N > 1.
```
斐波那契数列由 0 和 1 开始，之后的斐波那契数就是由之前的两数相加而得出。

答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。

## 示例1
```
输入：n = 2
输出：1
```
## 示例2
```
输入：n = 5
输出：5
```
## 方法：递归、动态规划
## 代码
```
class Solution:
    def fib(self, n: int) -> int:
        # 1、递归，但是可能会栈溢出，对于这道题，会出现超出时间限制
        # if n < 2:
        #     return n
        # return (self.fib(n-1) + self.fib(n-2)) % 1000000007
        # 2、动态规划
        if n < 2:
            return n
        last, last_next = 0, 1
        for i in range(2, n+1):
            res = last + last_next
            last = last_next
            last_next = res
        return res % 1000000007
```
求余运算法则：设有正整数x,y,p，则
```
(x + y) % p = (x % p + y % p) % p
```