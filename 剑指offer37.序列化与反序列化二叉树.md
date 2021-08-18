## 代码：
```
class Codec:

    def serialize(self, root):
        """Encodes a tree to a single string.
        
        :type root: TreeNode
        :rtype: str
        """
        if not root:
            return ''
        self.res = ''
        queue = collections.deque([])
        queue.append(root)
        while queue:
            node = queue.popleft()
            if node == None:
                self.res += 'null,'
                continue
            else:
                self.res += str(node.val) + ','
            if node.left:
                queue.append(node.left)
            else:
                queue.append(None)
            if node.right:
                queue.append(node.right)
            else:
                queue.append(None)
        return self.res.rstrip(',')
        

    def deserialize(self, data):
        """Decodes your encoded data to tree.
        
        :type data: str
        :rtype: TreeNode
        """
        if data == '':
            return None
        node = collections.deque(data.split(','))
        root = TreeNode(int(node.popleft()))
        queue = collections.deque([])
        queue.append(root)
        while queue:
            p = queue.popleft()
            if not p:
                continue
            nl = node.popleft()
            p.left = TreeNode(int(nl)) if nl != 'null' else None
            nr = node.popleft()
            p.right = TreeNode(int(nr)) if nr != 'null' else None
            queue.append(p.left)
            queue.append(p.right)
        return root
        

# Your Codec object will be instantiated and called as such:
# codec = Codec()
# codec.deserialize(codec.serialize(root))
```