---
title: Hash Tables
---
# Hash Tables
Store key/values based on hashing the key into another value, ideally evenly
distributed across the size of the hash table.

## Basic implementation (Java)
Notes:
* Hash function is very weak
* Uses open addressing technique for collision resolution
* Does not handle resizing
* Does not handle manipulations on full hash table

```Java
class HashTable<T> {
    private T[] values;
    private int[] keys;
    private int size;

    public HashTable(int size) {
        values = new T[size];
        keys = new Integer[size];

        for(int i = 0; i < size; i++){
            values[i] = null;
        }
    }

    public void put(int key, T value){
        int spot = findSpot(key);
        values[spot] = value;
        keys[spot] = key;
    }

    public T find(int key) {
        int spot = findSpot(key);
        return values[spot]; // will be null if not set
    }

    private int findSpot(int key){
        int hashIndex = hash(key);
        while(values[hashIndex] != null && key[hashIndex] != key){
            hashIndex = hash(hashIndex + 1);
        }
        return hashIndex;
    }

    private int hash(int key) {
        return key % size;
    }
}
```

## Choosing a Hash Function
TODO: fill me out

## Collision Resolution
### Separate Chaining
Separate chaining keeps each bucket independent, and maintains a list
of the elements that have been hashed to the bucket. Oftentimes,
a linked list is used. A variation of this includes the first value for the linked list in the bucket along with a pointer to the rest of the list.

### Open Addressing
With open addressing, each bucket holds only one element. If keys match, then the hash table generates a new index to try, until an empty bucket is found.
* Linear probing: interval between probes is fixed (e.g. increase index by 1)
* Quadratic probing: intervals between probes is increased by successive values of quadratic polynomial (e.g. attempt *x* increases *x-1* by 4*x*^3 + 2*x*^2 + 5*x* + 5)
* Double hashing: interval between probes is computed by another hash function

### Which is better?
Open addressing is better when records are small, and load factor is low.
Separate chaining is better when records are large (as space is only allocated for pointers to elements), or if load factor is higher (since less attempts to find an empty bucket)
