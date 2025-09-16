---
tags:
  - code
  - deno
  - typescript
  - python
  - binarysearch
  - algorithm
---
```typescript
function binarySearch(array: number[], value: number) {
    let low: number = 0;
    let mid: number = 0;
    let high: number = array.length - 1;
  
    while (low <= high) {
        mid = Math.floor((high + low) / 2);
  
        if (array[mid] < value) low = mid + 1;
        else if (array[mid] > value) high = mid - 1;
        else return mid;
    }
    return -1;
}
  
if (import.meta.main) {
    const array = [0, 2, 4, 6, 8, 10];
    console.log(binarySearch(array, 10)); // 5
    console.log(binarySearch(array, 0));  // 0
    console.log(binarySearch(array, 7));  // -1
}
```

```python
def binary_search(arr, x):
    low = 0
    high = len(arr) - 1
    mid = 0

    while low <= high:

        mid = (high + low) // 2

        # If x is greater, ignore left half
        if arr[mid] < x:
            low = mid + 1

        # If x is smaller, ignore right half
        elif arr[mid] > x:
            high = mid - 1

        # x is present at mid
        else:
            return mid

    # If we reach here, then the element was not present
    return -1
```