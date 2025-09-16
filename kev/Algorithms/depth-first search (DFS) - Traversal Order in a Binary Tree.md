---
tags:
  - binarytree
  - binarysearchtree
  - bst
  - algorithm
  - recursive
  - DFS
  - depthfirstsearch
---

## Traversal Order in a Binary Tree

A common task with binary trees is traversing the data structure, since without random access, this is the only way to do anything with our data: search, add, delete, print, etc. In addition to selecting an appropriate traversal algorithm, we also need to determine the order in which we want to visit the nodes.

At a high level, there are two types of traversals: **depth-first search (DFS)** and **breadth-first search (BFS)**. To explore these algorithms generally, you should read more about [DFS](https://interviewing.io/depth-first-search-interview-questions) and [BFS](https://interviewing.io/breadth-first-search-interview-questions). But in this article, we'll specifically discuss how traversal order is important for binary tree traversal.

DFS is a search algorithm that traverses a tree data structure by prioritizing exploring deeper paths from from child node to child node until a leaf node is finally visited or some condition is met. When visiting each node in a binary tree, the DFS algorithm has three operations it needs to perform in some order: "**visit the node**", which means perform some work (eg. print the value, add to some counter, delete it, etc), **traverse down the left subtree**, and **traverse down the right subtree**. The order of these three operations has a huge impact on the ultimate traversal order, so we further subdivide DFS into **preorder**, **inorder**, and **postorder** traversal.

As an alternative to DFS, [the BFS algorithm](https://interviewing.io/breadth-first-search-interview-questions) prioritizes visiting all the direct children at the same level before moving deeper into the tree. With this pattern, there is only one possible traversal order, which is called **level-order traversal**.

Let's explore these traversal orders more closely.

#### Inorder Traversal

Inorder traversal is a process for visiting each node in a binary tree by first visiting the left subtree, then the node itself, and then the right subtree. With **inorder traversal, the path always favors the leftmost tree before traversing the rest**.

![[Pasted image 20250912153929.png]]

The sequence produced with inorder traversal: 1, 3, 4, 6, 7, 8, 10, 13, 14.

In a binary search tree, inorder traversal **results in visiting the nodes in ascending order**. This is because by favoring resolving the left subtree at each node, at each node we are **always moving toward the smallest value available** and **returning the inorder successor**.

### Code example

```typescript
...
    printInOrder(): void {
        console.log('In-order traversal (sorted)');
        this._inOrderRecursive(this.root);
        console.log('\n');
    }
  
    private _inOrderRecursive(node: TreeNode<T> | null): void {
        if (node === null) return;
        this._inOrderRecursive(node.left);
        console.log(node.value);
        this._inOrderRecursive(node.right);
    }
...

if (import.meta.main) {
    const bst = new BinarySearchTree<number>();
  
    // Insert values (builds the tree)
    [50, 30, 70, 20, 40, 60, 80].forEach(val => bst.insert(val));
  
    // Print the sorted tree
    bst.printInOrder();
    // bst.preOrder();
    // bst.postOrder();
}
```

#### Preorder Traversal

Preorder traversal **visits each node in the tree by first visiting the node itself**, then **traversing the left subtree**, and **finally traversing the right subtree**. In each recursive call, the function first prints (or "visits") the current node, then calls the recursive function on the left subtree, and finally on the right subtree.

![[Pasted image 20250912154135.png]]

The sequence produced with preorder traversal: 8, 3, 1, 6, 4, 7, 10, 14, 13

### Code example

```typescript
...
    preOrder(): void {
        console.log('In-order traversal (sorted)');
        this._preOrderRecursive(this.root);
        console.log('\n');
    }
  
    private _preOrderRecursive(node: TreeNode<T> | null): void {
        if (node === null) return;
        console.log(node.value);
        this._preOrderRecursive(node.left);
        this._preOrderRecursive(node.right);
    }
...

if (import.meta.main) {
    const bst = new BinarySearchTree<number>();
  
    // Insert values (builds the tree)
    [50, 30, 70, 20, 40, 60, 80].forEach(val => bst.insert(val));
  
    // Print the sorted tree
    // bst.printInOrder();
    bst.preOrder();
    // bst.postOrder();
}
```

#### Postorder Traversal

In each recursive call, the function **first performs DFS on the left subtree**, **then performs DFS on the right subtree**, and **finally visits the current node**.

![[Pasted image 20250912154253.png]]

The sequence produced with postorder traversal: 7, 6, 4, 1, 3, 13, 14, 8

### Code Example

```typescript
...
    postOrder(): void {
        console.log('In-order traversal (sorted)');
        this._postOrderRecursive(this.root);
        console.log('\n');
    }
  
    private _postOrderRecursive(node: TreeNode<T> | null): void {
        if (node === null) return;
        this._postOrderRecursive(node.left);
        this._postOrderRecursive(node.right);
        console.log(node.value);
    }
...

if (import.meta.main) {
    const bst = new BinarySearchTree<number>();
  
    // Insert values (builds the tree)
    [50, 30, 70, 20, 40, 60, 80].forEach(val => bst.insert(val));
  
    // Print the sorted tree
    // bst.printInOrder();
    // bst.preOrder();
    bst.postOrder();
}
```

Postorder traversal is **often used to delete the nodes of a tree in a specific order**, because **we can easily reconstruct the node references**. We are basically **marking the exact path of the recursive calls by immediately printing each node as it is visited**.