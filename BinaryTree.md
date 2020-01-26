# Binary Tree Checklist

```python
# CLR: preorder recursive
def preorderRecursive(node:TreeNode):
    if node:
        visit(node)
        preorderRecursive(node.left)
        preorderRecursive(node.right)
    return

#CLR: preorder iterative - https://en.wikipedia.org/wiki/Tree_traversal
def preorderIterative(node:TreeNode):
    stack = [node]
    while stack:
        cur = stack.pop()
        visit(cur)
        if cur.right: stack.append(cur.right)
        if cur.left: stack.append(cur.left)
    return

# CLR: preoder iterative - my implementation
def preorderIterative(node:TreeNode):
    stack = []
    cur = node
    while stack or cur:
        if cur:
            visit(cur)
            stack.append(cur)
            cur = cur.left
        else:
            node = stack.pop()
            node = node.right
    return

# LCR: inorder recursive
def inorderRecursive(node:TreeNode):
    if node:
        inorderRecursive(node.left)
        visit(node)
        inorderRecursive(node.right)
    return

# LCR: inorder iterative DFS
def inorderIterative(node:TreeNode):
    stack = []
    cur = None
    while stack or cur:
        if cur:
            stack.append(cur)
            cur = cur.left
        else:
            node = stack.pop()
            visit(node)
            cur = node.right
    return

# LRC: postorder recursive
def postorderRecursive(node:TreeNode):
    if node:
        preorderRecursive(node.left)
        preorderRecursive(node.right)
        visit(node)
    return


    

```


  - Morrison

## Binary Tree characterstics

- depth
- height
- diameter

## Binary Search Tree

...
