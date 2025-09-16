---
tags:
  - code
  - datastructure
  - stack
  - array
---
## Requirements
- [[Linear Node]]

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

export class LinkedStack<T> {
    private head: LinearNode<T> | null = null;
    private _size: number = 0;
  
    constructor() {}
  
    push(value: T): void {
        const newNode = new LinearNode(value, this.head);
        this.head = newNode;
        this._size++;
    }
  
    pop(): T | null | undefined {
        if (this.isEmpty()) return undefined;
  
        const value = this.head!.value;
        this.head = this.head!.nextValue;
        this._size--;
        return value;
    }
  
    peek(): T | null | undefined {
        return this.head?.value;
    }
  
    isEmpty(): boolean {
        return this.head === null;
    }
  
    size(): number {
        return this._size;
    }
}

const myStack = new LinkedStack<number>();
console.log("Initial size:", myStack.size());
  
myStack.push(10);
myStack.push(20);
myStack.push(30);
  
console.log("Top element:", myStack.peek());
console.log("Size after pushes:", myStack.size());
  
console.log("Popped:", myStack.pop());
console.log("New size:", myStack.size());
console.log("Top element:", myStack.peek());
console.log("Is empty?", myStack.isEmpty());
```