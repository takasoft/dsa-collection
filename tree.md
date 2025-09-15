Assume the following data structure for this section.

```python3
# Definition for a binary tree node.
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None
```

## Find lowest Common Ancestor

```python3
def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
    res = None

    def dfs(node):
        nonlocal res

        if not node:
            return False

        leftFound = dfs(node.left)
        rightFound = dfs(node.right)
        currFound = node == p or node == q

        if leftFound and rightFound or leftFound and currFound or rightFound and currFound:
            res = node

        return leftFound or rightFound or currFound

    dfs(root)

    return res
```
