## 题目描述
输入某二叉树的前序遍历和中序遍历的结果，请重建该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。
## 示例
例如，给出
```
前序遍历 preorder = [3,9,20,15,7]
中序遍历 inorder = [9,3,15,20,7]
```
返回如下的二叉树：
```
    3
   / \
  9  20
    /  \
   15   7
```
## 方法
前序遍历：根节点|左子树|右子树

中序遍历：左子树|根节点|右子树

前序遍历序列第一个值就是根节点，然后根据根节点的值在中序遍历序列中找到根节点的索引，由此可以确定左树和右树的范围。
然后利用递归分别得到左树和右树。
## 代码
```
class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> TreeNode:
        if preorder == [] or inorder == []:
            return None
        self.dic = {val: idx for idx, val in enumerate(inorder)}
        self.preorder = preorder
        return self.process(0, 0, len(preorder)-1)

    def process(self, idx, left, right):
        """
        idx: 根节点在前序遍历中的索引
        left: 子树在中序遍历中的左边界
        right: 子树在中序遍历中的右边界
        """
        if left > right:
            return None
        root_val = self.preorder[idx]  # 根节点的值
        root_idx = self.dic[root_val]  # 根节点在中序遍历中的位置（索引）
        root = TreeNode(root_val)      # 根节点
        root.left = self.process(idx+1, left, root_idx-1)  # 左子树
        root.right = self.process(idx+root_idx-left+1, root_idx+1, right)  # 右子树
        return root
```