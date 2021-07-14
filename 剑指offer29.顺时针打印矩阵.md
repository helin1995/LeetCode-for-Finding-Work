## 题目描述
输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。
## 示例1
```
输入：matrix = [[1,2,3],[4,5,6],[7,8,9]]
输出：[1,2,3,6,9,8,7,4,5]
```
```
输入：matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
输出：[1,2,3,4,8,12,11,10,9,5,6,7]
```
## 思路
根据题意，我们知道顺时针打印矩阵的顺序：从左到右、从上到下、从右到左、从下到上。
那么，根据这个顺序，我们就能打印矩阵了。循环终止条件是：矩阵的点都打印了
## 代码
```
class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        if matrix == []:
            return []
        res = []
        total = 0
        top, down, left, right = 0, len(matrix), 0, len(matrix[0])
        size = len(matrix) * len(matrix[0])
        i, j = 0, 0
        while total < size:
            if i == top and j < right and total < size:
                while j < right:
                    res.append(matrix[i][j])
                    j += 1
                    total += 1
                i += 1
                j -= 1
                top += 1
            if j == right -1 and i < down and total < size:
                while i < down:
                    res.append(matrix[i][j])
                    i += 1
                    total += 1
                i -= 1
                j -= 1
                right -= 1
            if i == down - 1 and j == right - 1 and total < size:
                while j >= left:
                    res.append(matrix[i][j])
                    j -= 1
                    total += 1
                j += 1
                i -= 1
                down -= 1
            if i == down - 1 and j == left and total < size:
                while i >= top:
                    res.append(matrix[i][j])
                    i -= 1
                    total += 1
                i += 1
                j += 1
                left += 1
        return res
```