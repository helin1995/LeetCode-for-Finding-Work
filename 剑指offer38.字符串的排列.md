## 代码
```
class Solution:
    def permutation(self, s: str) -> List[str]:
        if not s:
            return []
        self.res = set()
        target = list(s)
        s = ""
        visited = [False] * len(target)
        def dfs(s, target, visited):
            if len(s) == len(target):
                self.res.add(s)
                return
            for i in range(len(target)):
                if visited[i]:
                    continue
                visited[i] = True
                dfs(s + target[i], target, visited)
                visited[i] = False
        dfs(s, target, visited)
        return list(self.res)
```