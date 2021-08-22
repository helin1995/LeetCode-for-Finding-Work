## 代码
```
class Solution:
    def constructArr(self, a: List[int]) -> List[int]:
        C = [1] * len(a)
        for i in range(1, len(a)):
            C[i] = C[i-1] * a[i-1]
        D = [1] * len(a)
        for i in range(len(a)-2, -1, -1):
            D[i] = D[i+1] * a[i+1]
        B = [1] * len(a)
        for i in range(len(a)):
            B[i] = C[i] * D[i]
        return B
```