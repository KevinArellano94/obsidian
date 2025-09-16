---
tags:
  - code
  - deno
  - typescript
  - python
  - slidingwindow
  - algorithm
---
```typescript
function maxSumSubArray(array: number[], k: number): number {
    if (array.length < k || k <= 0) throw new Error('Invalid input: array length must be >= k and k must be positive.');
  
    let windowSum: number = array.slice(0, k).reduce((sum, num) => sum + num, 0);
    let maxSum: number = windowSum;
  
    for (let i = k; i < array.length; i++) {
        windowSum = windowSum - array[i - k] + array[i];
        maxSum = Math.max(maxSum, windowSum);
    }
  
    return maxSum;
}
  
if (import.meta.main) {
    const numberArray: number[] = [1, 4, 2, 10, 2, 3, 1, 0, 20];
    const k: number = 4;
  
    console.log(maxSumSubArray(numberArray, k));
}
```

```python
def max_sum_subarray(arr, k):
    # Compute sum of the first window of size k
    # arr[:k] slices the array from index 0 to k
    window_sum = sum(arr[:k])
    max_sum = window_sum

    for i in range(k, len(arr)):
        # Compute sum of next window of size k by
        # removing the first element of the previous
        # window and adding the next element
        window_sum = window_sum - arr[i - k] + arr[i]
        max_sum = max(max_sum, window_sum)
    
    return max_sum
```