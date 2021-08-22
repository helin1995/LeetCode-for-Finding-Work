## 代码
```
class Solution:
    def nthUglyNumber(self, n: int) -> int:
        if n == 0:
            return n
        i, j, k = 0, 0, 0
        dp = [1] * n
        cur = 1
        while cur < n:
            minVal = min(dp[i] * 2, dp[j] * 3, dp[k] * 5)
            if minVal == dp[i] * 2:
                i += 1
            if minVal == dp[j] * 3:
                j += 1
            if minVal == dp[k] * 5:
                k += 1
            dp[cur] = minVal
            cur += 1
        return dp[-1]
```