## 题目描述
地上有一个m行n列的方格，从坐标 [0,0] 到坐标 [m-1,n-1] 。一个机器人从坐标[0, 0]
的格子开始移动，它每次可以向左、右、上、下移动一格（不能移动到方格外），也不能进入行
坐标和列坐标的数位之和大于k的格子。例如，当k为18时，机器人能够进入方格 [35, 37] ，
因为3+5+3+7=18。但它不能进入方格 [35, 38]，因为3+5+3+8=19。请问该机器人能够到达
多少个格子？
## 示例1
```
输入：m = 2, n = 3, k = 1
输出：3
```
## 示例2
```
输入：m = 3, n = 1, k = 0
输出：1
```
## 回溯法
思路同上一题
## 代码
```
class Solution:
    def movingCount(self, m: int, n: int, k: int) -> int:
        visited = []
        i, j = 0, 0
        res = self.process(visited, i, j, m, n, k)
        return res

    def bit_sum(self, num):
        s = 0
        while num != 0:
            s += num % 10
            num //= 10
        return s
    
    def process(self, visited, i, j, m, n, k):
        if i >= 0 and i < m and j >= 0 and j < n and (i, j) not in visited and self.bit_sum(i) + self.bit_sum(j) <= k:
            visited.append((i, j))
            count = 1 + \
                    self.process(visited, i-1, j, m, n, k) + \
                    self.process(visited, i+1, j, m, n, k) + \
                    self.process(visited, i, j-1, m, n, k) + \
                    self.process(visited, i, j+1, m, n, k)
            return count
        else:
            return 0
```