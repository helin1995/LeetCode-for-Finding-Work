## 题目描述：
在一个 n * m 的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个高效的函
数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

## 示例：
现有矩阵matrix如下：
```
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]

```

给定target=5，返回True。

给定target=20，返回False。

## 解题思路：O(m+n)、O(1)
根据题目描述，矩阵从左往右递增，从上往下递增。那么我们从矩阵的右上角开始，如果target等于右上角元素，那么直接返回True；
如果target小于右上角元素，那么只能在target的左侧寻找；如果target大于右上角元素，那么只能在target下方寻找。如果一直没有
找到，返回False。

## 代码：
```
class Solution:
    def findNumberIn2DArray(self, matrix: List[List[int]], target: int) -> bool:
        if matrix == [[]] or matrix == []:
            return False
        row, col = 0, len(matrix[0])-1
        while row < len(matrix) and col >= 0:
            if matrix[row][col] == target:
                return True
            elif matrix[row][col] > target:
                col -= 1
            else:
                row += 1
        return False
```