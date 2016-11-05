---
title: Mathematics
---

## Mathematics
#### Prime Numbers
###### Naive approach
```
boolean isPrime(int n){
    if(n < 2) {
        return false;
    }

    for(int i = 2; i < n; i++){
        if(n % i == 0){
            return false;
        }
    }

    return true;
}
```

###### Improvement
One thing to note is that you only actually need to check values to the square root
(since anything above the square root would have a smaller number that would be
the other multiple e.g. 10 = 2x5, only need to check through 4)

Additionally, you only need to check odd numbers since anything even is divisible by two.

```
boolean isPrime(int n){
    if (n < 2) {
        return false;
    }

    int sqrt = (int) Math.sqrt(n);
    for(int i = 3; i <= sqrt; i += 2){
        if (n % i == 0){
            return false;
        }
    }

    return true;
}
```

###### Sieve of Eratosthenes
Since all non-primes are divisible by primes, find primes and then iterate
through and cross off all multiples of that prime up to some max.

**Note**: this does not keep the odds-only check, that would be an optimization to add.

```
boolean[] sieveOfEratosthenes(int max){
    boolean[] flags = new boolean[max + 1];

    // set flags to true
    for(int i = 0; i < flags.length; i++){
        flags[i] == true;
    }

    int prime = 2;

    while(prime <= Math.sqrt(max)){
        // Cross off multiples
        for(int i = prime*2; i < max; i += prime){
            flags[i] = false;
        }

        // Get next prime
        int next = prime + 1;
        while(next < flags.length && !flags[next]){
            next++;
        }
        prime = next;

        // Break condition
        if(prime >= flags.length){
            break;
        }
    }

    return flags;
}
```

####Probability
###### Probability of P(A & B)
P(A & B) = P(B given A) P(A)

e.g. (when picking a number between 1 and 10, inclusive)
```
P(x is even and x <= 5) = P(x is even given x <= 5) P(x <= 5)
P(x is even and x <= 5) = (2/5) (1/2)
P(x is even and x <= 5) = 1/5
```

###### Probability of P(A | B)
P(A | B) = P(A) + P(B) - P(A & B)

```
P(x is even or x <= 5) = P(x is even) + P(x <= 5) - P(x is even and x <= 5)
P(X is even or x <= 5) = (1/2) + (1/2) - (1/5)
P(X is even or x <= 5) = 4/5
```

###### Independence
If A and B are independent, knowing one doesn't tell you anything about the
other.

P(A & B) = P(A) P(B), i.e. P(B given A) = P(B)

###### Mutual Exclusivity
If A and B are mutually exclusive, then the other cannot happen.

P(A | B) = P(A) + P(B), i.e. P(A & B) = 0

###### Combinatorics
Combinations: nCr (from n choose r) = n! / ((n-r)!r!)

Permutations: nPr (from n choose r, order matters) = n! / (n-r)!
