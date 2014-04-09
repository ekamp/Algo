#Exam 2 Review

##Greedy Algorithms
###Main Principle
Greedy algorithms build up to a solution peice by peice always choosing the solution that will yeild the most obvious and immediate benefit

###Coin Changing Problem US Currentcy
- The coin changing problem is the following : Someone wants to give change to a customer in coins whats the best way?
  - The highest coin is chosen that does not exceed the amount of change currently left to give.
  - This loop continues until there is no more change to give
  - For example if change is 35 cents then it starts by selecting a quarter which is 25 cents then a dime and so on

###Huffman Coding
<i>Huffman Coding is used to compress data in order to save space</i>
- In order to save space Huffman coding uses a prefix-free binary tree in order to encode
- In order to optimize the tree and save as much space as possible we want to make sure each leaf corresponds to a symbol
- In this method the number of bits required for a symbol is exactly the depth of the tree
- Alternatively we can calculate the cost by seeing that the frequency of any node is the sum of the frequencies of decendant leaves.
- <b>The cost of a tree is the sum of the frequencies of all leaves and nodes except the root.</b>
- <i>We also know that the lowest frequencies must be at the botton of the tree</i>
- To construct the tree first find the two nodes with the lowest frequency i and j and assign them to a node with the frequency i +j
- Continue this process until all frequencies are represented as leaves in the tree.
- Building the tree will take O(nlog(n)) time if a heap is used

###Horn Formulas
- A set of expressions with literals Implications and Negative Clauses
- Implications :
    - Left hand side is an AND of any number of positive literals
    - Right hand side is a single positive literal  (z^w) -> u
- Negative Clauses
  - Consists of an OR of any number of negative literals   (!u OR !v OR !y)
- Given the set of clauses the goal is to determine whether there is a consisten explaination that satisfies them
- <b>Strategy</b>
    - Start with all variables as false
    - Then we start to make some true one by one only to satify the implications (RHS)
    - Then turn to the negative clauses and make sure their satified
- If a certain set of variables is set tot true, then they must be true in any satisfying assignment.

###Set Cover
<b>Basically how many elements out of a set are needed to satisfy some condition</b>
- An example is suppose you have a set of schools Si and you want to see how many schools from the set will cover the country, essencially outputting a set of Sx Schools
- More generally we can see that B contains n elements and that the optimal cover consists of k sets, then the greedy will use (kln(n)) sets.
- <b>Strategy</b>
    - Use greedy to grab the largest sets first without going over the contraint
    - School example (grab school that covers the largest without going over and second largest w/o going over and so on)
- Let nt be the number of elements still not covered after t iterations, k sets are needed for optimal therefore nt/k extra will me needed.
- nt+1 <= nt - nt/k = nt(1 - 1/k)
- The approximation value of this greedy vs optimal is ln(n)

##Elements of Dynamic Programming

###Longest Increasing Subsequences
- Input : sequence of numbers a1...an
- Subsequence is a set of numbers and an increasing subsequence is one that increases from left to right
- For example 5,2,8,6,3,6,9,7 longest subsequence is 2,3,6,9 when put in graph form this is called a dag
- Once turned into a graph we want to find the largest subsequence by setting L(j) = 1 + max{L(i) : i,j within e} for each subproblem
- <b>Running Time</b>
    - Building the graph <i>O(n)</i>
    - Running n subproblems to find the result O(n<sup>2</sup>)

###Longest Common Subsequence
- Used to find the longest subsequence common to all subsequences in a set of sequences many times only two.
- This is used many times to compare two files within a file system also can be used to compare two strains of DNA
- Need to see if one sequence is a subsequence of another
- Given two sequences X and Y we say that Z is a subsequence of X and Y if Z is contained within both X and Y
- In the longest common subsequence given X and Y we wish to find the max length subsequence present in both x and y
<b>Procedure</b>
  - <b>Brute Force</b>
    - Enumerate all subsequences of X and check if it is a subsequence of Y
    - Since we have m subsequences this approach will take 2<sup>m</sup> time
  - <b>Recursion</b>
      - Assuming that c[i,j] is the length of the LCS
        - c[i,j] = 
          - 0 if i = 0 or j = 0
          - c[i-1,j-1] if i,j > 0 and x<sub>i</sub> = y<sub>j</sub>
          - max(c[i,j-1],c[i-1,j]) if i,j > 0 and x<sub>i</sub> != y<sub>j</sub>
</br>
<b>Finding the previous pointer for a digit</b>
- Find c[i,j] for x<sub>i-1</sub> and y<sub>j</sub>
- Find c[i,j] for x<sub>i</sub> and y<sub>j-1</sub>
- Determine the difference
</br>
- The runtime to find the longest common subsequence is O(X.length * Y.length)</br>
<b>Psedocode Find the Length of the LCS</b>
~~~c
  int m = X.length;
  int n = Y.length;
  let b[] and c[] be the new tables

  for(i = 1 to m)
  {
    c[i,0] = 0
  }
  for(j = 0 to n)
  {
    c[0,j] = 0
  }
  for(i = 1  to m)
  {
    for(j = 1 to n)
    {
      if(x<sub>i</sub> == y<sub>j</sub>
      {
        c[i,j] = c[i-1,j-1] + 1
        b[i,j] = c[i-1,j-1] + 1
      }
      else if(c[i-1,j] >= c[i,j-1]
      {
        c[i,j] = c[i-1,j]
        b[i,j] = c[i-1,j]
      }
      else
      {
        b[i,j] = c[i,j-1]
      }
    }
  }
  return c and b
~~~
<i>Running time for this is O(mn) since each entry takes O(1)</i>


###Finding the LCS of two strings or of two subsequences
- Finding the LCS of two strings hinders on two properties
    - First property (If the two strings end in the same character)
        - For example BANANA and ATANA
        - Remove and store the same last element until no common element between the strings is found, we find (ANA)
        - Now we look at the remaining seqences (BAN , AT)
        - Using inspection we see that the common sequences here is just A
        - Now append the removed elements to the element(s) found by inspection and we get out answer (AANA)
        - More formally we say that : 
            - x<sub>n</sub> = y<sub>m</sub> = LCS(x<sub>n</sub> , y<sub>m</sub>) = LCS(x<sub>n-1</sub> , y<sub>m-1</sub>)x<sub>n</sub>
    - Second Property (If the two strings do not end in the same character
        - We need to then find the LCS(x<sub>n-1</sub>,y<sub>m</sub>) and LCS(x<sub>n</sub>,y<sub>m-1</sub>)
        - For example we have X : ABCDEFG and Y : BCDGK, the LCD(X,Y) either ends in G or does not
            - Case ends in G
                - Therefore it cannot end in K so we remove k from the sequence Y getting BCDG, and now we can say that LCS(x<sub>n</sub>,y<sub>m</sub>) = LCS(x<sub>n</sub>,y<sub>m-1</sub>)
            - Case does not end in G
                - Then we remove G from X and get ABCDEF and therefore say that LCS(x<sub>n</sub>,y<sub>m</sub>) = LCS(x<sub>n-1</sub>,y<sub>m</sub>)
            - Therefore based on either case we are either looking for LCS(x<sub>n</sub>,y<sub>m-1</sub>) or LCS(x<sub>n-1</sub>,y<sub>m</sub>) which are both subsequences of X and Y therefore the longer one will become out LCS
</br>
<b>Strategy</b>
- Given two sequences X and Y
- If X and Y are equal return x<sub>n</sub>,y<sub>m-1</sub> or x<sub>n-1</sub>,y<sub>m</sub>
- Otherwise compare LCS(x<sub>n</sub>,y<sub>m-1</sub>) and LCS(x<sub>n</sub>,y<sub>m-1</sub>) continuing to compare until similarities are found and return the largest similarity

###Matrix Chain Multiplication
<i>Given a sequence or chain of A1...An of n matricies to be multiplied we wish to compute the product A1,A2...An</i>
- This multiplication is associative so all parenthesizations yield the same product
- <b>Fully Parenthesized</b> : if it is a single matrix or the product of two martricies surrounded by parens
- For example {A1,A2,A3,A4} can be fully parenthesized in the following way
    - (A1(A2(A3A4)))
    - (A1((A2A3)A4))
    - ((A1A2)(A3A4))
    - ((A1(A2A3))A4)
    - (((A1A2)A3)A4)
- We can multiply two matricies A and B only if they are compatible meaning that one matricy must have the same number of columns as the other matricy has rows.
- Due to this some groupings of chains are more efficient being that multiplying 100 rows 5 times is faster than multiplying 10 rows 5 times.
- <b>Matrix-chain multiplication problem</b> : given a chain of matricies {A1,A2,A3...An} fully parenthesize the product in a way that minimizes the number of scalar multiplications.
<b>Strategy</b>
- Take the sequence of matricies and seperate out into two subsequences
- Find the minimum cost of multiplying out the subsequences
- Add the costs together and the cost of multiplying the resultant frequencies
- Do this where each sequence can be split and take the minimum
- To make sure that it is O(n<sup>3</sup>) we have to use memorization to remember common pairs so we do not redundantly compute values
</br>
<b>Pseodocode</b>

~~~c
for(i = 1 to n)
{
  C(i,i) = 0
}
for(s = 1 to n-1)
{
  for(i = 1 to n-s)
  {
    j = i+s
    C(i,j) = min{C(i,k) + C(k+1,j) + m<sub>i-1</sub> * m<sub>k</sub> * m<sub>j</sub> : i <= k < j}
  }
  return C(1,n)
}

~~~

<b>Runtime O(n<sup>3</sup>)</b>

####Multiplication Given Dimensions
- Given the dimensions of matricies compute the number of operations necessary to multiply all of them together
- For example consider the matricies A<sub>1</sub>[10,100] , A<sub>2</sub>[100,5] , A<sub>3</sub>[5,50]
- In order to compute the number of operations needed to get the product of all the matricies we need to compute the different sets of multiplication as follows.
    - ((A<sub>1</sub>A<sub>2</sub>)A<sub>3</sub>) we compute 10 * 100 * 5 = 5,000 multiplications (A1 A2) the 10 * 5 * 50 2,500 for (A12 A3) = 7,500
        - Basically A1 * A2 will result in [A1.x,A2.y] then we do A1.x * A2.y * A3.y -> Prod 2 -> Answer = Prod1 + Prod2 
    - (A<sub>1</sub>(A<sub>2</sub>A<sub>3</sub>)) we compute 100 * 5 * 50 = 25,000 multiplications(A2,A3) and 100 * 50 * 100 = 50,000 -> 50,000 + 25,000 = 75,000 multiplications
    - Therefore from this result we see that we should choose the first grouping which takes 7,500 multiplications

###Knapsack Problem
- During a robbery  burglar finds much more loot than he intended on carrying and has to decide what to take
- His bag can hold w pounds, and there are n items of value v<sub>i</sub> and weight w<sub>i</sub>
- This can be solved in <b>O(nw)</b> time


<b>With Repetition</b>

- If we say that K(w) will give us the optimal solution we can assume the following
    - If item i is in the optimal solution set then we can remove i and say that the remainder items are K(w-w<sub>i</sub>) + v<sub>i</sub>
    - Since we do not know which i will result in the max solution we remove different items until a max is found
    - We continue this until all the weights have been explored and optimized
~~~c
  K(0) = 0 ;
  for(w = 1 to W)
  {
    K(w) = max{K(w-wi - vi) : wi <= w}
  }
return K(W)
~~~

<b>Without Repetition</b>
- Unlike before with repeptition we now have to consider if the item has been used before so we make sure 0 <= j <= n where j is the number of items.
- And now we say that K(w,j)  = max value using capacity w and number of items j
- Now its like before we need to see if the item needs to be in the optimal set so we say the following : 
    - K(w,j) = max { K(w - w<sub>j</sub> , j-1) + v<sub>j</sub> , K(w,j-1)}
- Now the algo involves filling out a 2d table and looks liike the following 
- Running time for this algo remains the same at O(nw)

~~~c
  //Initialize all K(0,j) = 0 and all k(w,0) = 0
  for(j = 1 to n)
  {
    for(w = 1 to n)
    {
      if(wj > w)
      {
        k(w,j) = k(w,j-1)
      }
      else
      {
        K(w,j) = max{ K(w,j-1), K(w-wj,j-1) + vj}
      }
    }
  }
  return K(W,n)
~~~
</br>
<b>Example Problem</b>
//none T_T

####Determining the number of subproblems
- If the input to a problem is x<sub>1</sub>...x<sub>n</sub> and the subproblems identified by a dynamic programming solution have the form x<sub>1</sub>...x<sub>i</sub>, i<= n how many subproblems exist? Similarly for inputs x<sub>1</sub>...x<sub>n</sub> and y<sub>1</sub>...y<sub>n</sub> where subproblems are x<sub>1</sub>,x<sub>i</sub>(1<=n) and y<sub>1</sub>...y<sub>j</sub>(j<=m). Similarly for input x<sub>1</sub>...x<sub>n</sub> and subproblems x<sub>i</sub>...x<sub>j</sub>
- Based on previous problems there should be i * n  subproblems taking O(ixn) time to run

##Graph Representations

###Adjancency Matrix Representation for Graphs
- Represented by an n x n array where the a<sub>ij</sub>th entry is a 1 if theres an edge from v<sub>i</sub> to v<sub>j</sub> and a 0 if there is no edge between v<sub>i</sub> and v<sub>j</sub>

####Advantages
- Presence of an edge can be found in constant time with only one memory access

####Disadvantages
- Takes O(n<sup>2</sub>) space to store the graph
- Many graphs are sparse in practice meaning they have relatively few edges

###Adjancency List Representation for Graphs
- The size of this representation is the size of the edges. Contains a linked list per vertex. The linked list for the vertex holds all verticies it has an outgoing edge to. This way an edge only appears once if directed or twice if undirected.

####Advantages
- Size of the graph representation is now O(|e|) where e is the number of edges
- Better for sparse graphs and in general takes less space

####Disadvantages
- Takes longer to iterate through to see if an edge is contained O(e) worst case

##Depth First Search
- Linear time procedure that finds what parts of the graph are reachable from a certain vertex

###Provide an algorithm that discovers in linear time the set of nodes in a graph reachable from a speciﬁc node. Argue about its correctness.
~~~c
  void explore(G(V,E) (graph with verticies V and edges E))
  {
    visited(u) = true;
    previsit(u)
    for(each edge in u : v)
    {
      if(!visited(v))
      {
        explore(v);
      }
    }
    postvisit(v);
    return : visited(u) is true for all nodes u reachable from v
  }
~~~
###Provide an algorithmic description for depth-ﬁrst search. What is its running time?
- Some small amount of work to mark a spot as visited and the pre and post visit
- A loop in which the adjacent edges are scanned to see if they lead somewhere new.
~~~c
  //First start off by marking everything as not visited
  for(all v element in V)
  {
    visited(v) = false;
  }
  //Then every verticy one away explore
  for(all v element in V)
  {
    if(!visited(v))
    {
      explore(v);
    }
  }
~~~
<b>Runtime</b></br>
- The first step of this will take O(v) time to go through all the vertices of the graph and mark them as visited
- The second step will take O(e) time because it visits the edges in explore x and explore y
- Therefore the total runtime of the algorithm is O(v + e)

###What is the pre-visit and post-visit order of nodes in depth-ﬁrst search?
- Previsit : The first time you see the vertex
~~~c
  void previsit(vertex v)
  {
    //Clock is our simple counter for the visitiing
    pre[v] = clock;
    clock++;
  }
~~~
- Postvisit : Once all edges have been explored and neighboring nodes visited
~~~c
  void postvisit(vertex v)
  {
    //Clock is our simple counter for the visitiing
    post[v] = clock;
    clock++;
  }
~~~

###How can depth-ﬁrst search be used in order to detect the connected components of a graph?
- <b>Connected graph</b> if theres a path from any verticy to another
- Trivially the DFS structure will detect this by using the counter on previsit and utilizing the adjacency matrix or list
- Therefore all we need to do is check that the ccnum[v] corresponds to the total number of verticies in teh graph. Each index in ccnumn is increased when a previsit occurs.

###You may be provided an undirected or directed graph, a start node and asked to provide the
search tree arising from a depth-ﬁrst search. You may also be asked to identify tree edges,
forward edges, back edges and cross edges (directed cases).
- <b>Creating the DFS Search tree</b>
    - When creating a DFS tree the root node is going to be your start node.
    - All of the verticies connected to the root node by an edge are considered the roots children or decendents and get placed below the root.
    - Then the children of the root or verticies connected to the root, also have children which are the verticies connected to them by an edge.
    - This continues until we run into verticies with no more edges and no more children
    - <b>Forward Edge</b> : lead from a node to a non-child decendent or in other words a grandchild or more
    - <b>Back Edge</b> : lead to an ancestor, go up one or more
    - <b>Cross Edge</b> : Lead to a node that is in the same node level and that has already been completely explored

###Show that a directed graph has a cycle if and only if its depth-ﬁrst search reveals a back edge.
- <b>Cycle</b> : In a graph is when a directed graph has a circular path
- One direction cycle is very easy to see if (u,v) is a back edge then there is a cycle consisting of this edge with the path from v to u in the search tree.
- Also by looking in the search tree if there is a particular node from v<sub>i-1</sub> to v<sub>i</sub> then a cycle exists due to this back edge.

###What is a directed acyclic graph (DAG)? What is the topological ordering of nodes in a DAG
and why it is useful?
- <b>Acyclic</b> : Graph without cycles
- We can test for Acyclic graphs in linear time
- <b>Directed Acyclic Graph (DAG)</b> : a graph that can be used to model causalities, hierarchies and temporal dependencies.
- <b>Topological Ordering of Nodes</b>
    - Each edge goes from an earlier vertex to a later vertex so that all procedence constraints are satisfied
    - All DAGs can be linearized, every edge leads to a vertex with a lower post number
    - This gives an O(n) time algo to order the edges in a DAG

###How is it possible to identify a sink node or a source node in a DAG using depth-ﬁrst search?
- Since all DAGs are linearized by their decreasing post numbers the vertex with the smallest post number must be a <i>sink</i> or in other words a node with no outgoing edges.
- Alternatively the vertex with the highest post number is a <i>source</i>, or a node with no incoming edges.

###What is the deﬁnition of strongly connected components? How is it possible to compute the decomposition of a directed graph into its strongly connected components? Provide an algorithm and argue about its running time.
- <b>Strongly Connected Components</b> : When two or more nodes are connected in both directions, have an innode coming in from every node within the component and an outnode going out to every node within the component.
- Can use depth first search which will decompose into strongly connected components in O(n) time
- <b>Facts</b>
    - If the explore subroutine is started at verticy u then it will terminate when all nodes reachable from u have been visited
    - The node that receives the highest post number in a DFS must lie in a source strongly connected component.
    - If C and C' are strongly connected components and there is an edge from a node in C to a node in C', then the highest post number in C is bigger than the highest post number in C'.
- <b>Procedure</b>
    - Find the sink by using the second and third fact and remove it from the graph
    - Run DFS on G<sup>r</sup>
    - Run the undirected connected components algo on G and during DFS process the verticies in decreasing order of their post number from step 1

##Breadth First Search


###Provide the algorithm that performs breadth-ﬁrst search on a graph. What is the inductive argument for the correctness of the approach? What is the running time of the algorithm?
~~~c
//dist(u) sets the distance of verticy u
  void BFS(Graph G, Vertex Start(s))
  {
    for(all u verticies in the graph)
    {
      dist(u) = infinity;
    }
    dist(s) = 0 ;
    Q = [s] (queue containing just s)
    while(Q is not empty)
    { 
      u = eject(Q);
      //This for goes over the current layer u and adds in the appropriate distance into the queue
      for(all edges(u,v) in the graph)
      {
        if(dist(v) == infinity)
        {
          inject(Q,v);
          dist(v) = dist(u) + 1;
        }
      }
    }
  }
~~~
- This algorithm will run in O(V+E) time

###What is the deﬁnition of a single-source shortest path problem? What is the deﬁnition of a single-destination shortest path problem? What is the deﬁnition of a single-pair shortest path problem? What is the deﬁnition of all-pairs shortest path problem? Which of these problems are equivalent? Do we know faster algorithms for the single-pair shortest path problem than the single-source shortest path problem?
- <b>Single Source Shortest Path Problem </b> : Finding the shortest path from a single starting vertex v to all other verticies within the graph
- <b>Single Destination Shortest Path Problem</b> : Finding the shortest path from all verticies in a graph to a single destination vertex v
- <b>Single-pair Shortest Path Problem</b> : Finding the path with the fewest edges.
- <b>All paits Shortest Path Problem</b> : Finding the shortest path between every pair of verticies v and v' in the graph.

###What is the “optimal substructure” property of shortest paths? Prove its validity
- If a node x lies on the shortest path from source node u to destination node v
- Then the shortest path from u to v is the shortest path from u to x and from x to v

###What happens with shortest paths on graphs that contain negative cycles? Can a shortest path contain positive cycles?
- Shortest path problems should not contain cycles because with the cycle with negative weight finding the path would be infinite, in other words there would be no min path
- Additionally the solution should not have any possitive cycles because those cycles can simply be removed giving the path a lower cost

##Dijkstra's Algorithm
###Provide Dijkstra's algo for computing single-sourced shortest paths. What is the requirement in order to be able to apply Dijkstra’s algorithm?

~~~c
  void dijkstra(G,l,s)
  {
    for(all u vertices)
    {
      dist(u) = infinity;
      prev(u) = nil;
    }
    dist(s) = 0;
    H = makequeue(V) ; //using distance values as the keys
    while(H is not empty)
    {
      u = deletemin(H);
      for (all edges (u,v))
      {
        if(dist(v > dist(u) + l(u,v))
        {
          dist(v = dist(u) + l(u,v);
          prev(v) = u;
          decreasekey(H,v);
        }
      }
    }
  }
  return u;
~~~
- Runtime : <b>O(E + vlog(v))
- Dijkstra's requires that there be edge weights and that a priority queue is used

###You may be provided an example graph and asked to return the search tree that arises from Dijkstra, as well as the state of the priority queue during its iteration of the algorithm.
- <b>Creating the search Tree</b>
    - Start off by adding the root or the start node into the table or tree
    - Then look at its outgoing edges and their weight, add the corresponding weights to the table
    - Then move on and look at the smallest current weight in the table not yet explored
    - Do the same thing except now overwrite all distances currently in the table with ones from the current node if the current node provides a cheaper path, and add in new nodes not yet seen
    - once all explored show the search tree which is just the graph with the shortest paths

###Prove the correctness of Dijkstra’s algorithm on non-negative weight graphs.
- Right?

###What is the best running time of Dijkstra’s algorithm and for what implementation of the priority queue data structure?
- The best running time for the algorithm is O(E + Vlog(V)) where E are the edges in the graph and V are the verticies in the graph. This running time is acheived using the fibonacci heap. However this is very complicated to implement and many times d-ary is more preferable with a O(v * d + E * lodv / logd)

###What is the running time of Dijkstra’s algorithm if the priority queue is implemented as a simple array? What is the running time of Dijkstra’s algorithm if the priority queue is implemented as a binary heap? When is each of these implementations preferred over the other?
- <b>Simple Array</b> : O(v<sup>2</sup>)
- <b>Binary Heap</b> : O((v + e)log(v))
- Depending on whether the graph is sparse or dense, in all graphs e < v<sup>2</sup>
- Single Array is preferable if e is close to v<sup>2</sup>
- Otherwise if e is  < v<sup>2</sup> / log(v) then binary heap is preferable


##Bellman-Ford and Floyd Warshall Algorithms
###Provide the Bellman-Ford algorithm for computing single-source shortest paths. What is the
running time of the approach and why? Why is it correct?
- This algorithm takes into consideration the shortest path given negative edge weights

~~~c
  //Graph G edge lengths l and start vertex s
  void shortestPath(G,l,s)
  {
    for(all verticies u)
    {
      dist(u) = infinity;
      prev(u) = nil;
    }
    dist(s) = 0 ;
    repeat |V| - 1 times
    {
      for(all edges)
      {
        update(e);
      }
    }
  }
~~~
- Running time : O(V*E)
- This is correct because it will update for each edge and not continue to loop if a negative cycle comes into play

###You may be provided a graph and asked to trace the dynamic programming matrix that arises from the operation of Bellman-Ford.
- Page 124 example in the book
- <b>Procedure</b>
    - Add root
    - Add neighbors and add their weight to the table
    - Rest is the same as Dijkstra's ???
###How can you detect the existence of negative cycles using the Bellman-Ford algorithm?
- If when creating the search table you end your search and see that the shortest path to a node is actually negative

###What is an efﬁcient approach for computing single-source shortest paths on directed acyclic graphs that may contain negative weight edges and what is the running time of this solution?
~~~c
  void dag-shortestPath(G,l,s)
  {
    for(all verticies)
    {
      dist(u) = infinity;
      prev(u) = nil;
    }
    dist(s) = 0 ;
    Linearize G
    for(each verticy in linearized order)
    {
      for(all edges(u,v))
      {
        update(u,v);
      }
    }
  }
~~~
- Runtime O(V + E)

###Why is the Floyd-Warshall algorithm preferred over calling V times the Bellman-Ford algorithm on a graph to solve all-pair shortest path problems?
- If we called V times the Bellman Ford algo on a graph to solve this we have the runtime of O(v<sup>2</sup>*e) instead of the quicker O(v<sup>3</sup>) Floyd-Warshall.

### What is the dynamic programming formulation of Floyd-Warshall, i.e., what are the subproblems deﬁned by the algorithm and how are they combined in order to address more complex problems?
- Look for a direct connection between node v and u
- If one does not exist expand your intermediate set to include more nodes until a connection is found
- Each time we expand we must again rexamine all the pairs to look for an already discovered intermediate shortest path
- This is easy because shortest from i to j using k and possibly others only uses k once assuming no cycles
- Additionally we already know the distance from i to k and k to j from previously

##Floyd-Warshall and Johnson's Algorithm
###Provide the Floyd-Warshall algorithm for solving all-pair shortest path problems. What is the running time of the approach?

~~~c
  for(i = 1 to n)
  {
      for(j = 1 to n)
      {
        dist(i,j,0) = infinity;
      }
  }
  for(all (i,j) edges)
  {
    dist(i,j,0) = l(i,j);
  }
  for(k = 1 to n)
  {
      for(i = 1 to n)
      {
        for(j = 1 to n)
        {
          dist(i,j,k) = min{dist(i,k,k-1) + dist(k,j,k-1) , dist(i,j,k-1)}
        }
      }
  }
~~~
- Runtime is O(V<sup>3</sup>)

###You may be provided a graph and asked to compute the dynamic programming matrix that arises from a few iterations of the Floyd-Warshall algorithm.
- First when creating the matrix number the top with 1->n and the left with 1->n
- Then label this as D0
- In D0 simply get the immediate distance or one node away distance from all verticies in the graph infinity if not reachable
- Then in D1 highlight the leftmost and topmost column
- You will be changing colmax-1 column
- Within those columns follow the following rules
    - If the previous number in the col was infinity then take the sum of the two numbers highlighted as the new value
    - If the previous number in the col was not infinity and your corresponding highlighted values are not inifinity then keep the previous number
    - if previous number was not infinity and one of the highlighted values are infinity replace the previous number with infinity
- On the second iteration move to the second leftmost and second topmost and repeat. Once you have reached the middle of the matrix apply the rules to all non-highlighted cols. Continue until you reach the bottom

###What is the transitive closure of a graph and how can it be computed following a dynamic programming approach? What is the relation to the Floyd-Warshall algorithm?
- <b>Transitive Closure of a graph</b> : The reachability of a graph, the extent to which you can reach a node from another node in the graph
- Can use Warshalls to find this closure by seeing how many rounds of warshalls it takes to populate the entire matrix without infinity distances. This is termed the connectivity matrix. This connectivity matrix can be derived from Warshalls

###If a graph has non-negative edges, is it preferable to run the Floyd-Warshall algorithm to solve an all-pair shortest path problem or is it preferable to call [V] times Dijkstra’s algorithm?
- Shouldn't matter, assuming that we use a simple array for Dijkstra's we see that one call of Dijkstra's yeilds O(v<sup>2</sup>) and if we call this v times we would get O(v<sup>3/sup>) the same runtime as Warshalls

###What is the main idea in Johnson’s algorithm and why can it be preferable over the Floyd algorithm when solving all pair shortest path problems
- <b>Johnson's Algorithm</b> : Find the shortest path between all pairs of verticies in a sparse edge weighted directed graph, allowing some of the edge weights to be negative.
- It is preferable over Warshalls because it removes all negative cycles and then uses Dijkstra's to label the graph. Reweights with no negative edges. This algo also runs in O(v<sup>2</sup>log(v) + v*e) which is faster than warshalls
<b>Procedure</b> : 
- A new node q is added to the graph connected by zero weight edges to each of the nodes in the graph
- The Bellman ford algo is used starting from the new vertex q to find each vertex v for the min weight h(v) of a path from q to v.
- The edges of the original graph are reweighted using the values computed by the bellman ford algo
- Finally q is removed and Dijkstras is used to find the shortest path from each node s to every other vertex v in the graph 


##Practice Questions
<i>Specify whether the following questions are true or false and explain why</i>
####An Adjacency matrix can quickly detect if an edge exists but the representation requires O(v<sup>3</sup>) space. A Ajancency list has space requirements of O(vlogv) but cannot detect whether an edge exists in constant time.
<i>False, because the an adjancency  matrix takes up O(v<sup>2</sup>) space and an adjancency list has space requirements of O(|v| + |e|)</i>

####Consider a general graph G(V,E). The best known algorithm for finding a path from a specific vertex s to a specific vertex t in G has better asymptotic running time than the best known algorithm for finding the paths for all verticies in V for a vertex t in G.
<i>False, They have the same runtime, Dijkstra's and an adjacency matrix both take O(v<sup>2</sup>) time</i>

####The shortest path cannot contain a zero weight cycle
<i>False, they can contain a zero weighted cycle because it won't effect the min cost of the path</i>

####Dijkstra's running time depends on the implementation of the priority queue data structure. An array implementation results in a running time of O(v<sup>2</sup>) and is prefered in dense graphs. A binary heap implementation results in O(vlogv + e) and is prefered in sparse graphs
<i>False the binary heap takes O((V + E)Log(v)), if we have a dense graph better to use an array and if we have a sparse graph better to use a binary heap</i>

####On a sparse graph with non-negative edges it is preferable to run |V| times Dijkstra's algorithm using a binary heap in order to compute the shortest paths between all pairs of nodes rather than running Warshall's which has a running time of &THETA(v<sup>3</sup>)
<i>True, if we simply look at the runtimes we can see that Dijkstra's with a binary heap runs faster with the runtime of O(V<sup>2</sup>log(v)) vs the runtime of Warshall's which takes O(V<sup>3</sup>)</i>

####You are transfering or robbing money from the bank and you already have filled n with cash. Each duffel bag i is unique. You are trying to fit the bags in the trunk of your car which has a volume of V, so as to maximize the amount of money that you can transfer in one trip. Provide a dynamic programming approach to this problem. (ID the subproblems and show how they are combined to solve larger problems
<i>Subproblems : We can use the volume V to define our subproblems, with volume V = 0 what is the max amount of money I can take and with which bags. Some with v = 1, v = 2 ... v. Additionally we need another variable to keep track of the volume of the current bag as to maximize the number of bags, the variable will be part of out optimal solution. </i>
~~~c
K(v,i) is the max value for v volume duffel bag i
if(V<sub>i</sub> > V)
{
  K(i,V) = K(V,i-1)
}
else
{
  K(i,V) = max{ K(V,i-1) , K(V-V<sub>i</sub>,i-1) + m<sub>i</sub>}
}
//At the end returning K(V,i)</br>
//This problem has the same guidelines as the Knapsack problem without repetion
~~~

####What is the runtime of the above dynamic programming solution and why
<i>O(iV), Since we defined our subproblems to be v = volume of the car and i = the amount of bags we have</i>

####A subsequence is pallindromatic if it is the same forwards as it is backwards. For instance the sequence, A,C,G,T,G,T,C,A,A,A,A,T,C,G has many pallindromatic sequences, including A,C,G,C, and A,A,A,A. Device an algorithm that takes the sequence x[1...n] and returns the length of the longest pallindromatic subsequence, its running time should be O(n<sup>2</sup>.

<i>This is the same as the Longest Common subsequence problem, the only difference would be that the first for will be reading from the right and the other for will be reading from the left</i>

~~~c
  //Assuming that S is the normal sequence and T is the reversed sequence
  for(i = 0 to n)
  {
    LPS(i,0) = 0; 
  }
  for(j = 0 to n)
  {
    LPS[0,j] = 0 ;
    for(i = 1 to n)
    {
      for(j = 1 to n)
      {
        if(Si == Tj)
        {
          LPS[i,j] = LPS[i-1,j-1];
        }
        else
        {
          LPS[i,j] = max{LPS(i-1,j),LPS(i,j-1)};
        }
      }
    }
  }
  return LPS[n,n]
~~~

####What is the definition of the strongly connected component?
<i>A strongly connected component is a set of 2 or more nodes that have a inode and an outnode to and from every node in the component</i>

####Provide the efficent algorithm for computing the decomposition of a directed graph into its strongly connected
- First need to find G<sup>R</sup>
    - We need to do this in order to run DFS and organize the nodes in a post-order increasing order
    - We have a property that says that the nodes with the highest post order is the source and the lowest post order are sinks, in other words they reverse G to get the sinks of the graph
    - Run the connected component alog of undirected graphs to find the connected components.
    - Since they are now organized according to the post order , I now have the sets of Strongly Connected Components thanks to algo in part two

####What is the running time of the efficent algorithm
- The running time is O(n)
