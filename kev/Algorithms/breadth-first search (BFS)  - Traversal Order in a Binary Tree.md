---
tags:
  - binarytree
  - binarysearchtree
  - bst
  - algorithm
  - recursive
  - BFS
  - breadthfirstsearch
time complexity: O(n)
space complexity: O(n)
---
## Traversal Order in a Binary Tree

A common task with binary trees is traversing the data structure, since without random access, this is the only way to do anything with our data: search, add, delete, print, etc. In addition to selecting an appropriate traversal algorithm, we also need to determine the order in which we want to visit the nodes.

At a high level, there are two types of traversals: **depth-first search (DFS)** and **breadth-first search (BFS)**. To explore these algorithms generally, you should read more about [DFS](https://interviewing.io/depth-first-search-interview-questions) and [BFS](https://interviewing.io/breadth-first-search-interview-questions). But in this article, we'll specifically discuss how traversal order is important for binary tree traversal.

DFS is a search algorithm that traverses a tree data structure by prioritizing exploring deeper paths from from child node to child node until a leaf node is finally visited or some condition is met. When visiting each node in a binary tree, the DFS algorithm has three operations it needs to perform in some order: "**visit the node**", which means perform some work (eg. print the value, add to some counter, delete it, etc), **traverse down the left subtree**, and **traverse down the right subtree**. The order of these three operations has a huge impact on the ultimate traversal order, so we further subdivide DFS into **preorder**, **inorder**, and **postorder** traversal.

As an alternative to DFS, [the BFS algorithm](https://interviewing.io/breadth-first-search-interview-questions) prioritizes visiting all the direct children at the same level before moving deeper into the tree. With this pattern, there is only one possible traversal order, which is called **level-order traversal**.

Let's explore these traversal orders more closely.

#### Level Order Traversal

As an alternative to using DFS we can also traverse a binary tree using Breadth-First Search (BFS), where we **visit each node belonging to the same level before moving deeper into the tree**. BFS uses a **queue data structure** (instead of a stack or recursion), in order to maintain the level-order traversal.

![[Pasted image 20250912161618.png]]

The sequence produced with level order traversal: 8, 3, 10, 1, 6, 14, 4, 7, 13

Level order traversal in a binary tree is **often applied to problems where we need to process tree nodes by level**, or if we want to **find the shortest distance between two nodes**.

### Code example

```typescript
...  
    levelOrderTraversal(): void {
        console.log('Level-order traversal (sorted)');
        this._levelOrderTraversal(this.root);
        console.log('\n');
    }
  
    private _levelOrderTraversal(node: TreeNode<T> | null): void {
        if (node === null) return;
  
        const queue: TreeNode<T>[] = [node];
  
        while (queue.length > 0) {
            const node = queue.shift()!;
            console.log(node.value + " ");
  
            if (node.left !== null) queue.push(node.left);
            if (node.right !== null) queue.push(node.right);
        }
    }
}
  
if (import.meta.main) {
    const bst = new BinarySearchTree<number>();
  
    // Insert values (builds the tree)
    [50, 30, 70, 20, 40, 60, 80].forEach(val => bst.insert(val));
  
    ...
  
    bst.levelOrderTraversal();
}
```

### Time and Space Complexity

Time complexity: `O(n)`, where n is the number of nodes. If we're not explicitly performing binary search, we will visit every node at worst in a traversal.

Space complexity: `O(n)`, additional space is needed on the call stack when performing recursion.