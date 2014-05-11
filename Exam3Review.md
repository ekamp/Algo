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
    - 
