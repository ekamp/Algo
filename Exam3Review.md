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
- General Algorithm : 
  - Continually add the lightest edge.
  - Before adding the lightest edge make sure it does not contain a cycle by making sure u - v canidates lie in a different component than end points u and v
  - More specifically we have the following : 
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
- In Kruskal's a safe edge is one that does not contain a cycle, is the lightest and is contained in a different cut than the rest of the graph.
- Running time of Kruskal's algorithm given we are using the disjoint set data structure. O(|E|log|v|)
- With the use of compression and union by rank we can get the runtime down to a little more than O(1) or in this case O(log(n)) runtime. Because the edge weights are smaller and upper bounded by O(|E|) we know that we can sort them in linear time. If we improve our data structure now using the union by rank we can reduce the time from logn to simply 1. Therefore we are left with O(|E|) for sorting and O(|E|) for the data structure per iteration. Therefore we wind up with a better runtime of O(|E|)
- makeset() (union by set)
  - 
- find()
  - Now when a series of parent pointer is followed to the root, we will change them so they point directly to the root
-
