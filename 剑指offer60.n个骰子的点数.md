## 代码
```
class Solution:
    def dicesProbability(self, n: int) -> List[float]:
        dp = [[0] * (6 * n + 1) for _ in range(n+1)]
        for i in range(1, 7):
            dp[1][i] = 1 / 6
        for i in range(2, n+1):
            for j in range(i, 6 * i + 1):
                temp = 0
                for k in range(1, 7):
                    if j - k > 0:
                        temp += dp[i-1][j-k] * 1 / 6
                dp[i][j] = temp
        return dp[-1][n:]
```