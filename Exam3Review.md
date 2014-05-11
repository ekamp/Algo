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
    //makeset(x); //Create a singleton set just containing x
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
