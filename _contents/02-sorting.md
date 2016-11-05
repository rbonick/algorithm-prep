---
title: Sorting
---

#### Sorting Algorithms

| Algorithm | Best Time | Average Time | Worst Time | Worst Space |
| --- | --- |
| Quicksort | O(n log n) | O(n log n) | O(n^2) | O(log n) |
| Mergesort | O(n log n) | O(n log n) | O(n log n) | O(n) |
| Heapsort | O(n log n) | O(n log n) | O(n log n) | O(1) |
| Tree Sort | O(n log n) | O(n log n) | O(n^2) |O(n) |
| Bubble Sort | O(n) | O(n^2) | O(n^2) | O(1) |
| Insertion Sort | O(n) | O(n^2) | O(n^2) | O(1) |
| Selection Sort | O(n^2) | O(n^2) | O(n^2) | O(1) |

## Sorting
#### Insertion Sort
1. Start at index 0
2. While not at end of array
    1. Get current index value
    2. Insert it into its correct place in the sorted section of the array
    3. Shift remaining sorted values down

#### Mergesort
Notes:
* Recursive
* Stable

1. Find midpoint of array, and split into two halves
2. Mergesort each half
3. Take resulting sorted arrays and merge them together
    1. Keep pointer to each
    2. Take smaller value until one array is empty
    3. Dump remaining array into end of new merged array

#### Heapsort
Notes:
* Not stable

The following uses a max heap, where the array is used like a pseudo tree with the following methods available:
* Parent(i) = floor(i/2)
* Left(i) = 2*i
* Right(i) = 2*i + 1

The only rule in a max heap is that an element's parent is greater than or equal to (>=) the element. (Min heap is the opposite)

1. Build Max Heap out of array
    1. Starting at the midpoint of the array to the start (index 0), `MAX HEAPIFY():`
        1. Get Left and Right children indices of current index
        2. If Left child is within bounds of the heap, and Left child is bigger than the current element,
            1. Largest is the Left child
        3. If Right child is within the bounds of the heap, and Right child is bigger than Largest,
            1. Largest is the right child
        4. If Largest is not the current element,
            1. Swap current element with the largest element
            2. Run `MAX HEAPIFY()` on the current element's new location (Largest's old location)
2. Starting at end of array, swap top of heap (biggest element, index 0) with current index *i*.
3. Max Heapify remaining elements (0 -> *i* - 1)

#### Quicksort
Notes:
* Recursive
* Not stable sort

1. Partition array
    1. Pick some element to be the pivot element
    2. Go through array
        1. If current element is smaller than the pivot,
            1. Swap with current pointer to end of smaller elements
            2. Increment pointer
        2. Swap pivot element with the pointer element
    3. Quicksort the left and right subarrays (leaving pivot in place).

#### Mergesort vs Quicksort
While both have similar average times, and quicksort has worse worst case time,
quicksort can be faster due to less overhead copying and merging arrays, as it
is in place.
