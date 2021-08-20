## 方法1：暴力解法
从1遍历到n，依次统计每个数中1的个数，然后累加，但是会超时
```
class Solution:
    def countDigitOne(self, n: int) -> int:
        times = 0
        for num in range(1, n+1):
            times += self.getTimesofOne(num)
        return times


    def getTimesofOne(self, n):
        t = 0
        while n:
            a, b = n // 10, n % 10
            if b == 1:
                t += 1
            n = a
        return t
```

## 方法2：规律
```
class Solution:
    def countDigitOne(self, n: int) -> int:
        res = 0
        temp = 1
        while temp <= n:
            res += (n // (10 * temp)) * temp + min(max(n % (10 * temp) - temp + 1, 0), temp)
            temp *= 10
        return res
```