## 题目描述
输入数字 n，按顺序打印出从 1 到最大的 n 位十进制数。比如输入 3，则打印出 1、2、3
一直到最大的 3 位数 999。

## 示例
```
输入: n = 1
输出: [1,2,3,4,5,6,7,8,9]
```

## 方法
全排列：n位数可以看作是0~9这10和数字的全排列，要得到从 1 到最大的 n 位十进制数，
我们可以从高位向低位递归，固定一个高位，然后对下一位进行递归，直到最低位。

## 代码
```
class Solution:
    def printNumbers(self, n: int) -> List[int]:
        num = ['0'] * n  # n位数字表示的字符列表
        res = []  # 最后的结果
        def dfs(digit):
            # 递归的终止条件是：到达最低位
            if digit == n:
                # 下面这个循环是将数字前面的0去掉，比如'001'去掉全面的0，变为'1'
                for j in range(n):
                    if num[j] != '0':
                        break
                s = int(''.join(num[j:]))
                if s != 0: res.append(s)
                return 

            for i in range(10):
                num[digit] = str(i)  # 固定高位
                dfs(digit+1)  # 对下一位进行递归
        dfs(0)  # 0是数字的最高位
        return res
```
## 笔记
如果遇到大数问题，可能会采用字符串来解题。