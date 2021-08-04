## 题目描述
输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历结果。如果是则返回true，否则返回false。假设输入的数组的任意两个数字都互不相同。

参考以下这颗二叉搜索树：
```
     5
    / \
   2   6
  / \
 1   3

```
## 示例1
```
输入: [1,6,3,2,5]
输出: false
```
## 示例2
```
输入: [1,3,2,6,5]
输出: true
```
## 思路
在后序遍历得到的序列中，最后一个数字是树的根节点的值。数组中前面的数字可以分为
两部分：第一部分是左子树节点的值，它们都比根节点的值小；第二部分是右子树节点的
值，它们都比根节点的值大。
## 代码：
```
class Solution:
    def verifyPostorder(self, postorder: List[int]) -> bool:
        if not postorder:
            return True
        root = postorder[-1]
        # 找到左子树的边界i-1
        for i in range(len(postorder)):
            if postorder[i] > root:
                break
        # 在右子树中判断是否所有的元素都比根节点的值大，如果是则进行
        # 下一步；如果不是，那么返回False
        for j in range(i, len(postorder)-1):
            if postorder[j] < root:
                return False
        # 对左右子树进行判断
        left = self.verifyPostorder(postorder[:i])
        right = self.verifyPostorder(postorder[i:-1])
        return left and right
```