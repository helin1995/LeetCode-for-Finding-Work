## 题目描述
请实现一个函数，把字符串 s 中的每个空格替换成"%20"。

## 示例
```
输入：s = "We are happy."
输出："We%20are%20happy."
```

## 方法1
使用python字符串内置方法replace(str1, str2)即用str2替换str1。面试的时候不能用这个方法。
## 代码
```
class Solution:
    def replaceSpace(self, s: str) -> str:
        # 方法1：使用python字符串内置方法replace(str1, str2)即用str2替换str1
        return s.replace(' ', '%20')
```
## 方法2
双指针法，原地替换。根据题目要求，我们要把字符串中的空格替换成'%20'，那么替换之后字符串的长度等于原来的长度加上2*空格
数目。因此，我们将原来的字符串增长，定义两个指针p1和p2。其中，p1指向原来字符串的末尾字符，p2指向增长后的（新的）字符串
的末尾字符。然后从后往前遍历p1，当p1指向非空格字符时，就将s[p1]赋值给s[p2]，p1和p2往前移动一格；当p1指向空格时，就
依次将'0'、'2'和'%'分别赋值给s[p2]、s[p2-1]和s[p2-2]，p1往前移动一格，p2往前移动3格。
## 代码
```
class Solution:
    def replaceSpace(self, s: str) -> str:
        p1 = len(s) - 1
        blank_nums = 0
        for c in s:
            if c == ' ':
                blank_nums += 1
        s = [c for c in s] + ['*'] * blank_nums * 2
        p2 = len(s) - 1
        while p1 >= 0:
            if s[p1] != ' ':
                s[p2] = s[p1]
                p1 -= 1
                p2 -= 1
            else:
                s[p2] = '0'
                s[p2-1] = '2'
                s[p2-2] = '%'
                p1 -= 1
                p2 -= 3
        return ''.join(s)
```
## 举一反三
在合并两个数组（包括字符串）时，如果从前往后复制每个数字（或字符）需要重复移动数字（或字符）多次，那么我们可以考虑
从后往前复制，这样就能减少移动的次数，从而提高效率。
