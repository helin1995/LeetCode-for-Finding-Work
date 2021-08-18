## 代码：
```
class Solution:
    def treeToDoublyList(self, root: 'Node') -> 'Node':
        if not root:
            return None
        self.pre = None
        self.head = None
        self.dfs(root)
        self.head.left = self.pre
        self.pre.right = self.head
        return self.head
    
    def dfs(self, cur):
        if not cur:
            return 
        self.dfs(cur.left)
        if self.pre == None:
            self.head = cur
            self.pre = cur
        else:
            self.pre.right = cur
            cur.left = self.pre
            self.pre = cur
        self.dfs(cur.right)
```