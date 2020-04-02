---
layout: page
title: Traversal
tags: DSA
---

The core of traversal is iteration.

     1
      \
       2
        \
         5
        /  \
       3    6
        \
         4

## Level Order Traversal

### Solution

```
def levelOrder(root):
	if root is None: return
	q = [root]
	while len(q)>0:
		n = q.pop(0)
		print(n.info, end=" ")
		if n.left: q.append(n.left)
		if n.right: q.appenf(n.right)
```