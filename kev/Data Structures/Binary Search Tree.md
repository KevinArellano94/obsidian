---
tags:
  - binarytree
  - binarysearchtree
  - bst
  - datastructure
  - recursive
  - nonerecursive
time complexity: O(log n)
space complexity: O(log n)
---
## What is a Binary Search Tree (BST)?

A common implementation of a binary tree is a **binary search tree**. Right there in the name, the binary search tree enables efficient implementation of the binary search algorithm thanks to the way the [[Binary Tree]] is organized: for each node in the tree, the value of the node is greater than the value of all the nodes in its left subtree and smaller than the value of all the nodes in its right subtree.

![[Pasted image 20250912071714.png]]

Due to the tree's binary search property, this structure **enables a systematic and efficient search process**. When searching for a target value, **comparisons are made at each node** to **determine whether to process the left or the right subtree**. This allows for the **elimination of half of the remaining search space at each step**, resulting in a **worst-case time complexity of O(log n)** for searching, where n is the number of nodes in the tree.

The height of a binary search tree affects the efficiency of the operations. Balanced binary search trees, such as AVL trees or Red-Black trees, maintain a balanced structure to ensure logarithmic time complexity for operations.

### Implementing a Binary Search Tree

To create a binary search tree, the insertNode method will enforce the binary search property. Traversing from the root, insertNode will recursively search for the correct position to add the new node by checking the binary condition: if the currentNode is larger than the new node, traverse left, if the currentNode is smaller than the new node, traverse right. Search will apply the same logic, but return if the target is found.

### Code example
#recursive

[[Tree Node]]

```typescript
export class TreeNode<T> {
    value: T;
    left: TreeNode<T> | null;
    right: TreeNode<T> | null;
    constructor(value: T) {
        this.value = value;
        this.left = null;
        this.right = null;
    }
}
  
export class BinarySearchTree<T> {
    root: TreeNode<T> | null;
    private comparator: (a: T, b: T) => number;
  
    constructor(comparator?: (a: T, b: T) => number) {
        this.root = null;
        this.comparator = comparator ?? ((a: T, b: T) => (a as any) - (b as any));
    }
  
    insert(value: T): void {
        if (!this.root) {
            this.root = new TreeNode(value);
            return;
        }
        this._insertRecursive(this.root, value);
    }
  
    private _insertRecursive(node: TreeNode<T>, value: T) {
        const compare = this.comparator(value, node.value);
  
        if (compare < 0) {
            if (node.left === null) {
                node.left = new TreeNode(value);
            } else {
                this._insertRecursive(node.left, value);
            }
        } else if (compare > 0) {
            if (node.right === null) {
                node.right = new TreeNode(value);
            } else {
                this._insertRecursive(node.right, value);
            }
        }
    }
    delete(value: T): void {
        this.root = this._deleteRecursive(this.root, value);
    }
  
    private _deleteRecursive(node: TreeNode<T> | null, value: T): TreeNode<T> | null {
        if (node === null) return null;
  
        const compare = this.comparator(value, node.value);
  
        if (compare < 0) {
            node.left = this._deleteRecursive(node.left, value);
        } else if (compare > 0) {
            node.right = this._deleteRecursive(node.right, value);
        } else {
            if (node.left === null) {
                // Case 1: 0 or 1 child (right only) -> Return right child
                return node.right;
            } else if (node.right === null) {
                // Case 2: Left only -> Return left child
                return node.left;
            } else {
                // Case 3: Two children -> Replace with in-order successor (min in right subtree)
                const successor = this._findMin(node.right);
                node.value = successor.value;  // Copy successor's value
                node.right = this._deleteRecursive(node.right, successor.value);
            }
        }
        return node;
    }
  
    private _findMin(node: TreeNode<T>): TreeNode<T> {
        while (node.left !== null) {
            node = node.left;
        }
        return node;
    }
  
    search(value: T): boolean {
        return this._searchRecursive(this.root, value);
    }
  
    private _searchRecursive(node: TreeNode<T> | null, value: T): boolean {
        if (node === null) return false;
        const compare = this.comparator(value, node.value);
        if (compare === 0) return true;
        if (compare < 0) return this._searchRecursive(node.left, value);
        return this._searchRecursive(node.right, value);
    }
  
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
  
    preOrder(): void {
        console.log('Pre-order traversal (sorted)');
        this._preOrderRecursive(this.root);
        console.log('\n');
    }
  
    private _preOrderRecursive(node: TreeNode<T> | null): void {
        if (node === null) return;
        console.log(node.value);
        this._preOrderRecursive(node.left);
        this._preOrderRecursive(node.right);
    }
  
    postOrder(): void {
        console.log('Post-order traversal (sorted)');
        this._postOrderRecursive(this.root);
        console.log('\n');
    }
  
    private _postOrderRecursive(node: TreeNode<T> | null): void {
        if (node === null) return;
        this._postOrderRecursive(node.left);
        this._postOrderRecursive(node.right);
        console.log(node.value);
    }
  
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
  
    // Print the sorted tree
    bst.printInOrder();
    bst.preOrder();
    bst.postOrder();
  
    // Search examples
    console.log('Search 40:', bst.search(40)); // true
    console.log('Search 90:', bst.search(90)); // false
  
    // New: Delete examples
    console.log('\n--- After deleting 30 (two children case) ---');
    bst.delete(30);  // 30 has left=20, right=40 -> Replaced by 40, delete 40
    bst.printInOrder();
  
    console.log('\n--- After deleting 20 (leaf) ---');
    bst.delete(20);  // 20 is now a leaf
    bst.printInOrder();
  
    console.log('\n--- After deleting 50 (root, one child) ---');
    bst.delete(50);  // Now root has only right child
    bst.printInOrder();
  
    console.log('Search 30 after delete:', bst.search(30)); // false
  
    bst.levelOrderTraversal();
}
```

#nonerecursive

TODO

[[depth-first search (DFS) - Traversal Order in a Binary Tree]]
[[breadth-first search (BFS)  - Traversal Order in a Binary Tree]]

### Practice questions

- https://interviewing.io/questions/find-leaves-of-binary-tree
- https://interviewing.io/questions/count-complete-tree-nodes
- https://interviewing.io/questions/recover-binary-search-tree
- https://interviewing.io/questions/binary-tree-upside-down