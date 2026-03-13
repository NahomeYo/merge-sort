# Merge Sort

## Complexity

- Best: O(n log n)
- Worst: O(n log n)
- Avg: O(n log n)
- Space: O(n)

## Problem Description

Merge sort is a divide-and-conquer sorting algorithm. Instead of trying to sort the entire array in one pass, it repeatedly splits the input into smaller halves, sorts those smaller parts recursively, and then merges the sorted halves back together into one final ordered result.

This strategy is powerful because once two halves are already sorted, combining them is much easier than sorting from scratch. The algorithm never depends on lucky input order, so it keeps the same strong runtime even on difficult or poorly arranged data.

## Code

```javascript
/**
 * Sort an array with merge sort and return a new sorted array.
 *
 * @param {number[]} values Input array.
 * @returns {number[]} Sorted array.
 */
function mergeSort(values) {
    if (values.length <= 1) {
        return values;
    }

    const mid = Math.floor(values.length / 2);
    const left = mergeSort(values.slice(0, mid));
    const right = mergeSort(values.slice(mid));

    return merge(left, right);
}

/**
 * Merge two sorted halves into one sorted array.
 *
 * @param {number[]} left Left sorted half.
 * @param {number[]} right Right sorted half.
 * @returns {number[]} Merged sorted output.
 */
function merge(left, right) {
    const sorted = [];
    let leftIndex = 0;
    let rightIndex = 0;

    while (leftIndex < left.length && rightIndex < right.length) {
        if (left[leftIndex] <= right[rightIndex]) {
            sorted.push(left[leftIndex]);
            leftIndex++;
        } else {
            sorted.push(right[rightIndex]);
            rightIndex++;
        }
    }

    // Append any leftover values from the unfinished half.
    return sorted.concat(left.slice(leftIndex), right.slice(rightIndex));
}

/**
 * Run the merge-sort demonstration.
 *
 * @returns {void}
 */
function main() {
    const array = [7, 3, 16, 12, 8];

    console.log("Original array =", array);
    console.log("Sorted array =", mergeSort([...array]));
}

main();
```

## Algorithm Steps

1. If the array has length 0 or 1, return it immediately because it is already sorted.
2. Find the middle index and split the array into a left half and a right half.
3. Recursively sort both halves.
4. Merge the two sorted halves by repeatedly taking the smaller front value.
5. Append any remaining values once one half is exhausted.
6. Return the merged sorted array.

## Explanation

The recursive structure of merge sort is what gives it its predictable performance. Each split cuts the array into smaller halves until the base case is reached, and then the algorithm rebuilds the full solution by merging sorted pieces together. Since the array is halved at every level, there are `O(log n)` recursive levels.

At each of those levels, the merge work across all subarrays totals `O(n)` because every element is copied into a merged result exactly once at that stage. Combining `O(n)` work per level with `O(log n)` levels gives a total runtime of `O(n log n)` in the best, average, and worst cases.

In the JavaScript code, `slice()` is used to split the input into the left and right halves, and `concat()` is used after the merge loop to attach whichever side still has values left. Those functions help make the code readable, but they also show why this version uses extra memory instead of sorting fully in place.

This implementation creates sliced halves and merged output arrays rather than sorting fully in place, so it uses `O(n)` extra space. That additional memory is the main tradeoff for merge sort's stable and consistently strong runtime.
