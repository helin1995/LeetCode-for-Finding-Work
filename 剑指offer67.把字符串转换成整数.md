## 代码
```
class Solution:
    def strToInt(self, str: str) -> int:
        if not str.strip():
            return 0
        start, cur = 0, 0
        for i in range(len(str)):
            if str[i] == ' ':
                continue
            if self.isValid(str[i]):
                start = i
                break
            else:
                return 0
        flag = True
        for i in range(start+1, len(str)):
            if str[i] >= '0' and str[i] <= '9':
                continue
            else:
                flag = False
                break
        end = len(str) if flag else i
        if str[start:end] == '+' or str[start:end] == '-':
            return 0
        else:
            res = int(str[start:end])
            if res >= -pow(2, 31) and res <= pow(2, 31) - 1:
                return res
            else:
                return -pow(2, 31) if res < 0 else pow(2, 31) - 1
    

    def isValid(self, c):
        if c == '+' or c == '-' or (c >= '0' and c <= '9'):
            return True
        else:
            return False
```