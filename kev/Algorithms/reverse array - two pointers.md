---
tags:
  - code
  - deno
  - typescript
  - python
  - reversearray
  - twopointers
---

```typescript
function reverseArray<T>(array: T[]): T[] {
    let start = 0;
    let end = array.length - 1;
  
    while (start < end) {
        const temp = array[start];
        array[start] = array[end]
        array[end] = temp;
        start += 1;
        end -= 1;
    }
    return array;
}
  
if (import.meta.main) {
    const numberArray = [0, 2, 4, 6, 8, 10];
    const stringArray = ['zero', 'two', 'four', 'six', 'eight', 'ten'];

    console.log(reverseArray(numberArray));
    console.log(reverseArray(stringArray));
}
```

```python
def reverse_array(arr):
    start = 0
    end = len(arr) - 1
  
    while start < end:
        arr[start], arr[end] = arr[end], arr[start]
        start += 1
        end -= 1
  
    return arr
```