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

###Approximation Algorithms
- Backtracking search in order to solve NP complete problems
  - The idea that we can reject a solution by only looking at a small portion of it
  - In otherwords if we know that a certain search space does not contain a solution we can prune it making our search space sig. smaller
  - We start off with a portion of the problem creating a partial solution and then branching into more and more solutions
  - As soon as we come to an assignment that violates our clause we prune it eliminating it from the search space and backtrack out to the parent partial solution
  - The general algorithm is as follows : 

~~~c
  Start with some initial problem P
  Let S = {P0}, the set of active subproblems
  Repeat while S is non-empty
    Choose a subproblem and remove it from S
    Expand it into smaller subproblems
    for each Pi :
      if test Pi succeeds halt and announce your solution
      if test Pi fails discard Pi
      otherwise add Pi to S
    Announce there is no solution
~~~

- Branch and Bound approach
  - Again like with SAT problems search problems too can be broken down into subproblems
  - In this case in order to reject a solution we need to see that its cost is greater than another solution
  - We however do not know the exact cost of the solution so we tend to use a quick lower bound approximation on the solution

~~~c
  Start with some problem P0
  Let S = {P0} the set of active subproblems
  bestSoFar = <Infinity></Infinity>
  Repeat while S is non empty
    Choose a subproblem P and remove it from S
    Expand it into smaller subproblems
    for each Pi
      if Pi is complete solution : update bestSoFar
      else if lowerbound(Pi) < bestSoFar : add Pi to S
    return bestSoFar
~~~

- Traveling Salesman with Branch and Bound approach
  - First create your partial solution passing through some of the verticies
  - Then branch from this adding a new edge to the partial solution noting that there can be V - S ways of doing this
  - The remainder of the tour is what remains or V - S therefore its cost is the sum of the following : 
       - Lightest edge from a to V - S
       - Lightest edge from b to V - S
       - Min spanning tree of V - S
- How is the approximation ratio computed?
  - Computed with the following : aA = max instance of algorithm A  / optimization of that instance
  - In other words this ratio measures the factor by which the algorithm A exceeds the optimum solution
  - So we are looking for this ratio to be as small as possible
- Approximation Ratio for Vertex Cover Problem
  - Better than greedy approach we can match a set of edges that have no common verticies and a set is said to be maximal if no edges can be added to it.
  - Maximal matching will help us find vertex covers faster
  - To generate this max matching we do the following : 
    - Repeatedly pick edges that that are disjoint from ones chosen already until no longer posible
    - Matching provides the lower bound on OPT
    - General solution to find vertex cover this way is as follows : 

~~~c
  Find a maximal matching M in E
  Return S = {all endpoints of edges in M}
~~~

- This will always produce a vertex cover at most twice that of the optimal solution or in otherwords has at most an approximation ratio of 2

###Local Search Heuristics
- How to tell when a distance problem is metric : 
  - The problem must fall into one of the three following properties : 
    - d(x,y) >= 0 for all x,y
    - d(x,y) = 0 if and only if x = y
    - d(x,y) = d(y,x)
    - Triangle inequality
- Clustering problem
  - Have some data that we want to divide into groups
  - Normally define distances between the groups and the data itself
  - We have n points in space and k spheres to cover them
  - Easiest way is to assign k points in space as sphere centers and assign the n points to the center closest to it
  - Centers are chosen being that each center should be as far as possible from the centers that have been chosen already

~~~c
  Pick any point u in X as the first cluster center
  for i = 2 to k
    let ui be in X farthest from u1...ui-1
  create k clusters : ci = {all x in X whose closest center is ui}
~~~

- To assign clusters to circles we define r or the distance from one center to another.
- Then we assign all clusters to a corresponding sphere that is of r distance
- When does a distance function satisfy metric properties?
  - When using clustering our approximation ratio corresponds to the ratio of the optimal radius to the actual radius
  - In this case the worst case we can have for the approximation ratio is 2r

- Traveling Salesman Approximation Ratio
  - If its edge weights satisfy the metric properties then the TSP can result in a 1.5 approximation ratio using the following algorithm.

~~~c
  Given any Graph G
    Compute I(G,C) with C = n * a and run algorithm A on it
    if the resulting tour has length < n*a
      Conclude that G has a Rudrata path
    else it has no Rudrata path
~~~

- This then proves that there can exist a polynomial time solution to TSP
- Unless in the case P = NP there cannot exist a polynomial time solution to TSP

- General Local Search Framework
  - The algo looks like as follows :

~~~c
  let s be an initial solution
  while there is some solution s' in the neighborhood of s
    for which cost(s')< cost(s) : replace s by s'
  return s
~~~

- Local Search on Traveling Salesman
  - Each tour will take into consideration O(n^2) neighbors
  - Can use n-change searches in which graphs are generated that differ by three paths
  - When we use more and more differences we increase our chances of finding an oprimal solution

- Local Search Graph Partitioning
  - Input is an undirected graph and an integer between 0 and 1/2
  - Output : a partition of the verticies into two groups
  - First we can split into two evenly starting by switching verticies accross the cut

- Local Search Optima
  - Randomization
    - Can be used to find a random local solution or choose a local move when several are avalible
    - If there is a possiblity of finding a local solution represented as p then over 1/p runs a solution will be found
    - More repetitions of a local search starting at a random solution has a decreasing probability of finding the optimal solution
  - Simulated Annealing
    - Increase the cost in hopes that the search will get opt solution
    - Introduces the temperature T
    - If T is 0 then it is the same cost of the previous example, but if T is large it has a varying cost from the original
    - Trick is to start with a large T and generally reduce it to zero checking if you have found the optimal solution or not
    - Increases the amount of movement you make but in many cases increases the chance of finding an optimal solution

~~~c
  let s be any starting solution
  repeat
  randomly chose a solution s' in the neighborhood of s 
  if the change in the cost(s') and cost(s) is negative 
    replace s by s'
  else
    replace s by s' with probability e^(-delta/T)
~~~
