## 代码
```
class Solution:
    def translateNum(self, num: int) -> int:
        num = str(num)
        return self.dfs(0, num)
    

    def dfs(self, point, num):
        if point >= len(num):
            return 1
        if point+1 < len(num) and num[point] + num[point+1] >= '10' and num[point] + num[point+1] <= '25':
            return self.dfs(point+1, num) + self.dfs(point+2, num)
        else:
            return self.dfs(point+1, num)
```