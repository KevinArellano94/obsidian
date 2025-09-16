---
tags:
  - datastructure
  - binarytree
---

## What is a Binary Tree?

A binary tree is a type of [tree data structure](https://interviewing.io/trees-interview-questions) where each node can have **at most two children**, typically referred to as the **left child** and the **right child**. This binary structure allows for **efficient searching**, **insertion**, and **deletion** operations, especially when further rules are applied to the tree to express different types of binary trees.

![[Pasted image 20250912070511.png]]
### Code example

```typescript
export class BinaryTreeNode {
    left: BinaryTreeNode | null = null;
    right: BinaryTreeNode | null = null;
    data: number | null = null;
  
    BinaryTreeNode(value: number): void {
        this.data = value;
    }
}
```

Given that not all nodes need to have two children, binary trees can be **tall** or **wide**, and everything in between. If each node in a binary tree only has one child (except for leaves), the tree would be much taller than it is wide. On the other hand, if most or all the nodes in a binary tree have two children, then the tree would be considered balanced.

Specifically, we can view binary trees as being balanced or unbalanced by this measure: a binary tree is balanced when the heights of the left and right subtrees of any node **differ by at most one**. The height of a tree is determined by the number of edges in the longest path from the root to a leaf.

![[Pasted image 20250912071017.png]]

The main advantage of a balanced binary tree is that we can achieve optimal performance for searching, adding and deleting operations - by maintaining logarithmic height, these operations can be performed in **O(log n) time complexity on average**.

Examples of balanced binary trees are **AVL trees** and **Red-Black trees**. These are considered advanced topics, sometimes found in database implementations along with other use-cases, and rarely come up in interview questions. More often, when discussing binary tree optimizations, we encounter binary search trees.