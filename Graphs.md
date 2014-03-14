#Algo Graph Theory

##Graphs

G(V,E)
- V is the vertices of the graph
- E is the edges of the graph

###Adjacency Graph Matrix

- |V| = n
- A = nxn
- ay will be 1 if it is an adjacency and 0 otherwise

<u>Undirected Graph</u>
- A is summetric
- This will take O(n^2) space

###Adjacency List

|Node|Connections|
|----|----------:|
|A   |D          |
|B   |C->D       |
|C   |B->E       |
|D   |A->B->E    |
|E   |C->D       |

- Now this only takes O(n) space assuming it is sparse
- Lookup now becomes O(n)