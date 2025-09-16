---
tags:
  - code
  - datastructure
  - binarytree
  - treenode
---
## Code example

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
```