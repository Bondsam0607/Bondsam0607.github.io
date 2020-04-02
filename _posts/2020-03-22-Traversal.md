---
layout: page
title: Traversal
tags: DSA
excerpt_separator: <!--more-->
article_header:
  type: overlay
  theme: dark
  background_color: '#123'
  background_image: false
---

The core of traversal is iteration.

<!--more-->

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