---
layout: post
title: Binary Tree
date: "2020-10-11 13:30:00 -0700"
tags: [interview, algorithm]
---

## 前序遍历

### 递归
三要素：
1. 函数参数和返回值
2. 终止条件
3. 单层递归的逻辑

以前序遍历为例
```
res = []
def traversal(root):
    if not root: # 终止条件
        return
    res.append(root.val) # 前序
    traversal(root.left)
    traversal(root.right)
```

### 迭代（栈）
```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def preorderTraversal(self, root: TreeNode) -> List[int]:
	from collections import deque

        queue = deque()
        queue.append(root)
        res = []

        while queue:
            curr = queue.pop()
            if not curr:
                continue
            res.append(curr.val)
            queue.append(curr.right)
            queue.append(curr.left)
        return res
```

## 后序遍历
从前序遍历修改而来，前序是中左右，这里先调整为中右左，最后将result反转即可。
```
class Solution:
    def preorderTraversal(self, root: TreeNode) -> List[int]:
	from collections import deque

        queue = deque()
        queue.append(root)
        res = []

        while queue:
            curr = queue.pop()
            if not curr:
                continue
            res.append(curr.val)
            queue.append(curr.left)
            queue.append(curr.right)
        return res[::-1]
```

## 中序遍历
中序遍历不能从前序遍历修改而来，原因是前序是先访问中间节点同时先处理中间节点，而中序是后处理中间节点。


```
def inorderTraversal(self, root: TreeNode) -> List[int]:
    queue = deque()
    res = []

    curr = root
    while curr or queue:
        if curr:
            queue.append(curr)
            curr = curr.left
        else:
            curr = queue.pop()
            res.append(curr.val)
            curr = curr.right
    return res
```

## 层序遍历
前中后遍历都是DFS，层序是BFS。
将每一层的节点入堆，因此这里需要双重循环。
```
class Solution:
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
        if not root:
            return []
        from collections import deque
        queue = deque()
        res = []
        queue.append(root)

        while queue:
            level = []
            size = len(queue)
            for _ in range(size):
                curr = queue.popleft()
                if not curr:
                    continue
                level.append(curr.val)
                queue.append(curr.left)
                queue.append(curr.right)
            if level:
                res.append(level)
        return res
```
