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


###Graph Search
- Given V and S is there a path from V to S
- Process over the entire graph using dykstras
<b>Procedure</b> : Explore (G,v) where G is the input graph and v is the start vertex
       


       Explore(G,v)
              Visited (v) = true
              Previsit (v),
              for each edge (u,y) there exists T
              {
                if (visited u == false)
                {
                  Explore (G,u)
                }
                post visit(v)
              }

- Solid edges actually traversed during the search
- Dotted edges are not traversed
- Can we use the explore proceedure to find the number of connected components in a forest
- Start a counter, set number of connected components to 0, mark all verticies as not visited, start explore(x) which is initially random.
- Increment number of connected components and call the explore function again but on a verticy that has not been visited.

###Depth First Search

              DFS(g)
       for all v set to not visited -> visited(v) = false
       for v in verticy list
       {
              if(!visited)
              {
                     explore(G,v)
              }
       }

<u>Running Time</u>
- How many times is each vertex visited?
       - Constant number of times
       - We also loop over all edges
       - <b>O(|v|+|e|) where v is the number of vertices and e is the number of edges

- Ancestor : (eg : A is a ancestor of b or t
       - A : ancestor
       - c : child
- pre(a) < pre(c) < post(c) < post(a)

- Forward edges :  Edges part of the DFS
- Back edges : Edges not traversed
- Cross Edges : :Ead neither to a desendant or ancester

<b>DFS Tree</b>
<u>(U,v)</u>
</br>[ [ ] ] Forward edge</br>
u v v u</br>
</br>
[ [ ] ] Back edge</br>
v u u v</br>
</br>
[ ] [ ] Cross edge</br>
u u v v</br>
</br>
- The relationships can be inclusive or disjoint


###Directed Acyclic Graphs
- Cycle : x0 -> xn -> x0
- We can actually check with dfs whether a graph has a cycle or not.
- Everytime you discover a back edge there is a cycle

<b>Proof</b>
- If (u,v) is a back edge
- u ancestor of v
[ [ ] ]
v u u v
- There is a path from v to u that dfs has already discovered and is different than (u,v) this path together with (u,v) forms a cycle.
- Opposite is true as well : if g contains a cycle then lets deine as xi the vertex that has the lowest precounter during the dfs. 
- All xj in the cycle xj != xi are reachable from xi and are going to be decendants in the dfs tree. including xi-1
- Therefore we also know that (xi-1,x1) will be a back edge.

<b>DAGs</b> : define an implicit ordering over the verticies.
- Properties : in a DAG every edge leads to a vertex with a lower post order
- ie no back edges and no cycles
- Corollary : the vertex with the smallest post number meaning it has no outgoing edges, it is a sink.
- The vertex with the highest post order meaning it has all outgoing edges and no incoming edges meaning that this is a source.
- The DAG only contains sources and sinks
- Each DAG has at least one source and at least one sink

<b>Different way of computing the ordering on a DAG is to</b>
- First find a source
- Delete the source from the graph
- Repeat until the graph is empty

<u>Strongly Connected Components</u>
- Be able to move from one component to another basically cycles in the graph
- 
