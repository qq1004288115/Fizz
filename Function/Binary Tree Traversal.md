## 总结
 * 递归
 * 栈
    * 每次入栈一个子节点
    * 每次入栈左右节点

## Preorder
每次入栈一个子节点
```
def preorder(root):
    stack = []
    ans = []
    while stack or root:
        while root:
            ans.append(root.val)
            stack.append(root)
            root = root.left
        root = stack.pop().right
    return ans
```

```
def preorder(root):
    stack = []
    ans = []
    while root or stack:
        if root:
            ans.append(root.val)
            stack.append(root)
            root = root.left
        else:
            root = stack.pop()
            root = root.right
    return ans
```
每次入栈左右节点
```
def preorder(root):
    if not root: return []
    stack = [root]
    ans = []
    while stack:
        node = stack.pop()
        ans.append(node.val)
        if node.right:
            stack.append(node.right)
        if node.left:
            stack.append(node.left)
    return ans
```

## Inorder
每次入栈一个子节点
```
def inorder(root):
    stack = []
    ans = []
    while stack or root:
        while root:
            stack.append(root)
            root = root.left
        root = stack.pop()
        ans.append(root.val)
        root = root.right
    return ans
```

```
def inorder(root):
    ans = []
    stack = []
    while stack or root:
        if root:
            stack.append(root)
            root = root.left
        else:
            root = stack.pop()
            ans.append(root.val)
            root = root.right
    return ans
```
每次入栈左右节点
```
def inorder(root):
    if not root: return []
    ans = []
    stack = [(root, False)]
    while stack:
        node, flag = stack.pop()
        if node:
            if flag:
                ans.append(node.val)
            else:
                stack.append((node.right, False))
                stack.append((node, True))
                stack.append((node.left, False))
    return ans
```
## Postorder
每次入栈左右节点
```
def postorder(root):
    s = []
    if not root: return s
    stack = [root]
    while stack:
        cur = stack.pop()
        s.insert(0, cur.val)
        if cur.left:
            stack.append(cur.left)
        if cur.right:
            stack.append(cur.right)
    return s 
```
```
class Solution:
    def postorderTraversal(self, root):
        traversal, stack = [], [(root, False)]
        while stack:
            node, visited = stack.pop()
            if node:
                if visited:
                    # add to result if visited
                    traversal.append(node.val)
                else:
                    # post-order
                    stack.append((node, True))
                    stack.append((node.right, False))
                    stack.append((node.left, False))

        return traversal
```
每次入栈一个子节点
```
def post(root):
    ans = []
    stack = []
    while stack or root:
        while root:
            ans.insert(0, root.val)
            stack.append(root)
            root = root.right
        root = stack.pop().left
    return ans
```
```
def postorder(root):
    ans = []
    stack = []
    pre = None
    while root or stack:
        if root:
            stack.append(root)
            root = root.left
        else:
            node = stack[-1]
            if not node.right or node.right == pre:
                stack.pop()
                pre = node
                ans.append(node.val)
            else:
                root = node.right
    return ans
```

```
class Solution:
    def postorderTraversal(self, root: TreeNode) -> List[int]:
        ans = []
        stack = []
        while root or stack:
            while root:
                stack.append([root, False])
                root = root.left
            root, flag = stack[-1]
            if flag:
                stack.pop()
                ans.append(root.val)
                root = None
            else:
                stack[-1][1] = True
                root = root.right
        return ans
```
