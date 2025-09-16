---
tags:
  - code
  - datastructure
  - linearnode
---
## Code example

```typescript
export class LinearNode<T> {
    constructor(
        public value: T | null = null,
        public nextValue: LinearNode<T> | null = null
    ) {}
}
```