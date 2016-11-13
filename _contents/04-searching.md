---
title: Searching
---
# Searching
Binary search is most common, but can also use a tree or hash table to search.
Keep in mind runtime!

### Binary Search
To find an element in a **sorted** array, compare the element's value to the midpoint
of the array. If larger than the midpoint value, search to the right of the midpoint
recursively, and vice versa on the left. If the value matches, then return the
index of the midpoint.
