Exam 3 Review
===================
##Minimum Spanning Trees
- Typically seen as trees they are used to find the min cost network say in a network of computers
- This graphs / trees are undirected
- They cannot contain cycles because removing an edge from a cycle would reduce cost without reducing connectivity
<b>Properties</b>
- Removing a cycle edge cannot disconnect the graph
- A tree of n nodes has n-1 edges
- Any connected undirected graph G = (V,E) with E = V - 1 is a tree
- An undirected graph is a tree if and only if there is a unique path between any pair of nodes


###Greedy Approach / Kruskal's
- A general algorithm for this is as follows : 
  - Continue to add the next lightest edge to the graph until all are connected

###Cut Property
- Partition of the verticies into 2 groups S and V - S. Always safe to add the lightest edge
- An edge cuts accross the cycles of a graph
- The lightest edge is the edge of min weight that connects accross the cut of S and V-S

###Kruskal's and Prim's algorithm
####Kruskal's algorithm
- General Algorithm 
  - Continually add the lightest edge.
  - Before adding the lightest edge make sure it does not contain a cycle by making sure u - v canidates lie in a different component than end points u and v
  - More specifically we have the following 

  ~~~c
    //makeset(x); //Create a singleton set just containing X
    //find(x); //to which set does x belong, check their components
    //union(x,y); //merge the set of x and y
    
    for (u in V)
    {
      makeset(u);
    }
    Sort all the edges E by weight
    for (all edges {u,v} in E in increacing order of weight)
    {
      if(find(u) != find(v)
      {
        add edge {u,v} to X;
        union(u,v);
      }
    }
  ~~~

- General Runtime of Kruskal's is O(mlog(m)) bounded by how fast we can sort
- In Kruskal's a safe edge is one that does not contain a cycle, is the lightest and is contained in a different cut than the rest of the graph.
- Running time of Kruskal's algorithm given we are using the disjoint set data structure. O(|E|log|v|)
- With the use of compression and union by rank we can get the runtime down to a little more than O(1) or in this case O(log(n)) runtime. Because the edge weights are smaller and upper bounded by O(|E|) we know that we can sort them in linear time. If we improve our data structure now using the union by rank we can reduce the time from logn to simply 1. Therefore we are left with O(|E|) for sorting and O(|E|) for the data structure per iteration. Therefore we wind up with a better runtime of O(|E|)
- makeset(x) (union by set)
  - Makes a set from a single item
- find(x)
  - Now when a series of parent pointer is followed to the root, we will change them so they point directly to the root
  - Finds the set x belongs to
- union(x,y)
  - Unions the set x and y

####Prims Alogorithm

- A set of nodes X constantly grows by the lowest cost edge between our explored or current subtree and the subtree not yet explored.

~~~c
  X = {} //edges picked so far
  repeat until |X| = |V| - 1 :
    pick a set S in V for which X has no edges between S and V-S
    let e in E be the minimum weight edge between S and V-S
    X  = X U {e}
~~~

- This is extremely similar to Dijkstras except that the ordering of the priority queue in Prims is ordered by the value of the lightest incoming edge and Dijkstra's is just ordered by the cost of the path and the current weighting.
- They are so similar that their runtimes are the same, therefore : 
    - Simple array : O(v<sup>2</sup>)
    - Binary Heap : O(|E| + |V|log(|V|))

###NP Complete Reduction
- What is the Minimum cut problem, and what is its runtime?
  - A cut of the graph that has the smallest weight or number of elements, in this case we are looking for the smallest weight.
  - We can get the smallest or min cut by removing the last edge that Kruskal's adds to the span
  - This finds the min cut with a prob of 1/n<sup>2</sup> so if we repeat n<sup>2</sup> we will find it
  - Therefore we repeat n<sup>2</sup> times to get our result making the runtime O(n<sup>2</sup>mlog(n))
  - Some further tuning brings this down to O(n<sup>2</sup>log(n))
- What is the balanced cut problem ?
  - Given a graph with n verticiesand budget b partition the vertices into two sets T and S in which |S|, |T| >= n/3 and there are at most b edges between S and T. 
  - Such problems are used for clustering, such as  segmenting an image into certain components
  - Best way to do this is to have a node for each pixel and segment similar color pixels that are close to each other.
  - A balanced cut would be say seperating an elephant from the sky within a photo
  - There is no polynomial time algorithm for finding the balanced cut of a graph
- What is the knapsack problem?
  - A robber has broken into a store and wants to fill a bag of size V with n items each worth v. Wants to maximize v and only has V space. 
  - If the robber can take the same item can be solved in O(nW) time
  - If the robber cannot take the same item repeatedly can be solved in O(nW) time
  - Subset sum
      - More generally this is given a set of integers is there a subset whose sum is a specific number s
      - This is NP complete problem that is a specialized version of knapsack bcause it can be used to keep track of the number of items and their weights that add up to the max weight the robber can carry
- What is the class of NP problems? 
    - There are two classes NP hard and NP easy, NP easy can be solved efficently and NP hard cannot
    - The class of all search problems are termed NP.
    - The class of all search problems solvable in polynomial time are termed P
    - If P = NP we would be able to solve all search problems in polynomial time, that is why it is widely beleived that p != NP
    - A search problem is NP-complete if all other search problems reduce to it.
- What does it mean to reduce search problem A into search problem B?
    - It means we are translating one search problem into another
- What do you need to provide such a reduction?
    - Polynomial time algorithm that transfers and instance of A into an instance of B
    - Polynomial time algorithm that maps  a solution s of A back into a solution h(s) of B
- When is a problem in the class co-NP problem?
    - When its complement is an NP problem
    - co_NP is when the answer is no
    - An example of this is if we want to find a min cut from a graph with one node
    - Many times these problems are both NP and co-NP

###Examples of Reductions NP Complete
- 3-SAT to Independent Set
  - Set of clauses each with 3 or less literals
  - We aim to find a satisfing truth
  - First we create a triangle for each clause because we have 3 literals per clause
  - Then choose a goal g to be the number of clauses
  - Then to prevent choosing opposite literals as the same boolean we put an edge between all opposite literals
  - If g < the number of verticies we cannot determine the truth of the 3SAT
  - Otherwise we assign a certain vertex x to be be true and therefore x! is false
  - Therefore if a clause has x it is said to be true or if it contains x! it is false
- SAT to 3-SAT
  - Modify the statement in order to remove clauses that have >= 4 literals per clause
  - Converting these requires polynomial time and a new variable to replace the few that we junked I to I'
  - {a<sub>1</sub> V a<sub>2</sub> V ... a<sub>k</sub>} => { (a<sub>1</sub> V a<sub>2</sub> V y<sub>1</sub>) V ... (a<sub>k-1</sub> V a<sub>k</sub> V y<sub>k-3</sub>)
- Independent Set to Vertex Cover
  - Set of nodes S is a vertex cover of graph G that is S touches every edge E in G, if and only if V-S are independent set in G
  - First look for vertex cover of G with V - g nodes.
  - If it exists take all nodes not within the cover
  - Otherwise if it doesnt exist then the conversion cannot be made.
- Independent Set to Clique
  - First define the complement of a graph G to be G' = (V,E!) where E! contains unordered pairs of verticies not in E
  - Then S is an independent set of G if and only if S is a clique of G'.
  - These nodes have no edges between them if and only if they have all possible edges in them in G'
  - So all we need to do is map an instance (G,g) of Independent Set to the corresponding instance (G',g) of Clique
- Circuit SAT to SAT
  - We need to rewrite in conjunctive normal form or in other words the AND of clauses
  - For each gate g we create a variable g and model the effect of the gate with the following : 
    - We add additional clauses and AND them together in order to produce the same result
    - This is important because all problems can reduce to Cirucuit SAT then we can further reduce them to SAT so they are easier to work with.
    - We can do this conversion in Polynomial time
