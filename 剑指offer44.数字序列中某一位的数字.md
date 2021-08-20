## 代码
```
class Solution:
    def findNthDigit(self, n: int) -> int:
        if n < 10:
            return n
        total = 9
        k = 1
        while True:
            if total < n:
                total += 9 * (10 ** k) * (k + 1)
                k += 1
            else:
                break
        k -= 1
        total -= 9 * (10 ** k) * (k + 1)
        n -= total
        a, b = n // (k + 1), n % (k + 1)
        start = 10 ** k + a
        if b == 0:
            return int(str(start-1)[-1])
        else:
            return int(str(start)[b-1])
```