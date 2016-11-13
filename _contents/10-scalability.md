---
title: Scalability
---

# Scalability
Scalability problems are fairly straightforwards.

1. Make believe - solve for an infinitely powerful computer, no memory limitations
2. Get real - how much can fit on a single machine? What issues occur when splits occur?
3. Solve problems - solve the issues identified in step 2.

#### Dividing Up Data
* By order of appearance - when current machine is full, add another. Can result
in very large lookup tables
* By hash value - choose a key and hash it, storing on a machine based on the result.
No lookup tables, but how to handle when a machine is full? Can either shift data
around, very expensive, or split data into two machines causing a tree structure
of machines.
* By actual value - no need to hash, can just store based on actual data. For example,
social network might keep someone living in Mexico in Mexican servers, since most
of their friends are probably also in Mexico.
* Arbitrary - just arbitrarily break up the data, keeping a lookup table.
