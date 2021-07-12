## 题目描述
请实现一个函数，用来判断一棵二叉树是不是对称的。如果一棵二叉树和它的镜像一样，那么它是对称的。

例如，二叉树 [1,2,2,3,4,4,3] 是对称的。
```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```

但是下面这个 [1,2,2,null,3,null,3] 则不是镜像对称的:
```
    1
   / \
  2   2
   \   \
   3    3
```
## 示例1
```
输入：root = [1,2,2,3,4,4,3]
输出：true
```
## 示例2
```
输入：root = [1,2,2,null,3,null,3]
输出：false
```
## 思路
二叉树的遍历方式有三种：前序遍历、中序遍历和后序遍历。这三种遍历方式都是先遍历
左子树，然后遍历右子树。那么我们可以尝试另一种遍历方式，先遍历右子树，然后遍历
左子树。

那么，如果一棵树是对称的，那么它的前序遍历（这里以前序遍历为例），和它的对称
前序遍历所得到的序列是一样的。但是，遍历的时候一定要包含null节点。因为不包含
null节点，两种遍历方式可以得到相同的序列，即使不是对称树。比如第二个例子。

第二个例子的前序遍历结果（不包含null节点）为：1,2,3,2,3

第二个例子的对称前序遍历结果（不包含null节点）为：1,2,3,2,3

但是这棵树不是对称的。而考虑了null节点之后两种遍历的结果分别为：

前序遍历：1,2,null,3,2,null,3

对称前序遍历：1,2,3,null,2,3,null

那么，我们可以看到考虑了null节点之后，得到的序列是不相等的。因此，这棵树不是对称的。

## 代码
```
class Solution:
    def isSymmetric(self, root: TreeNode) -> bool:
        if root == None:
            return True
        def process(root1, root2):
            if root1 == None and root2 == None:
                return True
            if root1 != None and root2 == None:
                return False
            if root2 != None and root1 == None:
                return False
            if root1.val == root2.val:
                return process(root1.left, root2.right) and process(root1.right, root2.left)
            else:
                return False
        return process(root, root)
```