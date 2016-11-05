---
title: NP Complete problems
---

### NP-Complete problems
Essentially, problems whose solutions can be verified in polynomial time

###### Boolean Satisifiability Problem (SAT)
Whether the variables of a Boolean formula can be replaced by true/false in such
a way that the formula evaluates to true;

Examples:
* Satisfiable: A and not B
* Unsatisfiable: A and not A

###### Knapsack Problem
Given a set of items, each with a weight and value, determine number of items
to include in a collection so that the total weight is less than or equal to
a given limit.

Note: can be solved in psuedo-polynomial time with dynamic programming. Still
NP-Complete since it is O(nW) where n is number of items and W is total weight;

###### Hamiltonian Path Problem
Whether a Hamiltonian path (path in a graph that visits each vertex exactly
once) or cycle exists in a given graph.

###### Traveling Salesman Problem
Given a list of cities and the distances between them, find the shortest
path that visits each city exactly once and returns to the origin.

Nearest Neighbor can yield an effectively short route but is can be flawed and
yield a very bad result.

###### Subgraph Isomorphism Problem
Two graphs are given as input, and it must be determined whether one contains a
subgraph that is isomorphic to the other (isomorphic = all vertices can be
matched up so that the paths between nodes are the same).

###### Subset Sum Problem
Given a set of integers, is there a non-empty subset whose sum is zero?

Pseudo-polynomial solution exists by keeping track of which values sum to zero.
Q(i, s) is a boolean function that determines if there exists a subset from
x0 to xi which sums to s. Runtime is O(sN)
```
Q(1, s) = x1 == s
Q(i, s) = Q(i-1, s) || (xi == s) || Q(i-1, s - xi)
```

###### Clique Problem
Finding a clique (complete subgraph, so all vertices are adjacent to all vertices).

Can find maximal (**not maximum**) by starting with a clique and adding a vertex
if it connects to all members of current clique and discarding it otherwise.

Cliques of fixed size: runs in O(n^k k^2): polynomial if k is fixed

###### Vertex Cover
Vertex cover is a subset of a graph such that every edge has at least one
endpoint in the vertex cover. A minimum vertex cover is the smallest vertex
cover in a graph.

###### Independent Set
Independent or stable set is a set of vertices in a graph with none of the
vertices adjacent to each other.

Maximal independent set is either an independent set such that adding any
vertex to the set forces it to contain an edge, or the set of all vertices in
the graph.

Maximum independent set is the largest possible independent set, and finding one
is NP-Complete. Very similar to the clique problem, as a clique is an independent
set in the complement graph.

###### Dominating Set
Dominating set is the set of vertices such that all vertices *not* in the set
are adjacent to at least one member of the set.

Related to independent sets: a maximal independent set is a dominating set and
is the only type of independent set that is also dominating. The minimum
dominating set is not necessarily independent, but it is less than or equal
to the size of a minimum maximal independent set.

###### Graph Coloring
Coloring the vertices of a graph such that no two vertices share the same color,
or can be edges or faces also.

Can always be colored, but minimum number of colors vary. If a clique of size
*k* exists, there must be at least *k* colors.

Determining if a graph can be colored by only two colors exists in linear time.

Can be solved with dynamic programming but not in polynomial time.

Greedy coloring is just adding a new color if all colors are used by an
adjacent vertex.
