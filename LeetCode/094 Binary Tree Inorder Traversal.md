## Recursive
```
class Solution:
    def inorderTraversal(self, root: TreeNode) -> List[int]:
        res = []
        def f(x):
            if not x:
                return
            else:
                f(x.left)
                res.append(x.val)
                f(x.right)
        f(root)
        return res
```
------------------------------------------------
## Stack
```
class Solution:
    def inorderTraversal(self, root: TreeNode) -> List[int]:
        res = []
        stack = []
        cur = root
        while  cur or stack:
            while cur:
                stack.append(cur)
                cur = cur.left
            cur = stack.pop()
            res.append(cur.val)
            cur = cur.right
        return res
```

## Morris Traversal
```
class Solution:
    def inorderTraversal(self, root: TreeNode) -> List[int]:
        res = []
        cur = root
        while cur:
            if not cur.left:
                res.append(cur.val)
                cur = cur.right
            else:
                left = temp = cur.left
                while left.right:
                    left = left.right
                cur.left = None        # pay attention!
                left.right, cur = cur, temp
        return res
```
        