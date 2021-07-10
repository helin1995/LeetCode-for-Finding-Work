## 题目描述
请实现一个函数用来匹配包含'. '和'*'的正则表达式。模式中的字符'.'表示任意一个字符，
而'*'表示它前面的字符可以出现任意次（含0次）。在本题中，匹配是指字符串的所有字符匹
配整个模式。例如，字符串"aaa"与模式"a.a"和"ab*ac*a"匹配，但与"aa.a"和"ab*a"均不
匹配。

## 示例1
```
输入:
s = "aa"
p = "a"
输出: false
解释: "a" 无法匹配 "aa" 整个字符串。
```
## 示例2
```
输入:
s = "aa"
p = "a*"
输出: true
解释:因为 '*' 代表可以匹配零个或多个前面的那一个元素, 在这里前面的元素就是 'a'。
因此，字符串 "aa" 可被视为 'a' 重复了一次。
```

## 方法：动态规划，具体解释看代码
```
class Solution:
    def isMatch(self, s: str, p: str) -> bool:
        # 动态规划：dp[i][j]表示s[:i]、p[:j]是否匹配
        m, n = len(s) + 1, len(p) + 1  # 加1的目的是引入s和p都是空字符串的情况
        dp = [[False] * n for _ in range(m)]  # 初始化dp数组
        for i in range(m):
            # 当模式p为空时，不能匹配
            dp[i][0] = False
        dp[0][0] = True  # 当s和p都为空时，可以匹配
        for j in range(2, n, 2):
            # 当s为空时，只有当p的偶数位（第一个字符下标为1开始算）为*时可以匹配
            if p[j-1] == '*' and dp[0][j-2]:
                # 加入dp[0][j-2]这个条件是为了保证p[:j-2]是空的（可以匹配s）
                dp[0][j] = True
        for i in range(1, m):
            for j in range(1, n):
                if p[j-1] == '*':
                    # 当p[j-1]为*时：
                    # 1、如果dp[i][j-2]为True，即s[:i]与p[:j-2]匹配，那么s[:i]、p[:j]匹配，因为*可以使得*前面的字符出现0次
                    # 2、如果dp[i-1][j]为True，即s[:i-1]与p[:j]匹配，那么就要看s[i-1]是否与p[j-2]也就是*前面的字符匹配
                    if dp[i][j-2]:
                        dp[i][j] = True
                    elif dp[i-1][j] and (s[i-1] == p[j-2] or p[j-2] == '.'):
                        dp[i][j] = True
                    else:
                        dp[i][j] = False
                else:
                    # 如果p[j-1]不为*，就看dp[i-1][j-1]即s[:i-1]和p[:j-1]是否匹配，如果匹配，就看s[i-1]和p[j-1]是否匹配
                    if dp[i-1][j-1] and (p[j-1] == s[i-1] or p[j-1] == '.'):
                        dp[i][j] = True
                    else:
                        dp[i][j] = False
        return dp[-1][-1]
```
